---
title: "Incorporación de una partición con herramientas de bases de datos elástica | Microsoft Docs"
description: "Establece cómo usar las API de escala elástica para agregar particiones nuevas a un conjunto de particiones."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 62a349db-bebe-406f-a120-2f1986f2b286
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 6a91ea2251ea3b748faba5c97765bfded9c00234
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="adding-a-shard-using-elastic-database-tools"></a><span data-ttu-id="aa146-103">Incorporación de una partición con herramientas de bases de datos elásticas</span><span class="sxs-lookup"><span data-stu-id="aa146-103">Adding a shard using Elastic Database tools</span></span>
## <a name="to-add-a-shard-for-a-new-range-or-key"></a><span data-ttu-id="aa146-104">Para agregar una partición para un nuevo intervalo o clave</span><span class="sxs-lookup"><span data-stu-id="aa146-104">To add a shard for a new range or key</span></span>
<span data-ttu-id="aa146-105">Con frecuencia, las aplicaciones simplemente necesitan agregar nuevas particiones para controlar los datos que se esperan de nuevas claves o intervalos de claves, en un mapa de particiones que ya existe.</span><span class="sxs-lookup"><span data-stu-id="aa146-105">Applications often need to simply add new shards to handle data that is expected from new keys or key ranges, for a shard map that already exists.</span></span> <span data-ttu-id="aa146-106">Por ejemplo, es posible que una aplicación particionada por identificador de inquilino necesite aprovisionar una nueva partición para un nuevo inquilino o que datos particionados mensualmente necesiten que se aprovisione una nueva partición antes del inicio de cada nuevo mes.</span><span class="sxs-lookup"><span data-stu-id="aa146-106">For example, an application sharded by Tenant ID may need to provision a new shard for a new tenant, or data sharded monthly may need a new shard provisioned before the start of each new month.</span></span> 

<span data-ttu-id="aa146-107">Si el nuevo intervalo de valores de clave no forma parte todavía de una asignación existente, es muy sencillo agregar la nueva partición y asociar la nueva clave o el nuevo intervalo a dicha partición.</span><span class="sxs-lookup"><span data-stu-id="aa146-107">If the new range of key values is not already part of an existing mapping, it is very simple to add the new shard and associate the new key or range to that shard.</span></span> 

### <a name="example--adding-a-shard-and-its-range-to-an-existing-shard-map"></a><span data-ttu-id="aa146-108">Ejemplo: incorporación de una partición y su intervalo a una asignación de partición existente</span><span class="sxs-lookup"><span data-stu-id="aa146-108">Example:  adding a shard and its range to an existing shard map</span></span>
<span data-ttu-id="aa146-109">En este ejemplo se utilizan los métodos [TryGetShard](https://msdn.microsoft.com/library/azure/dn823929.aspx), [CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx) y [CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn807221.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeShardMap`1.CreateRangeMapping\(Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeMappingCreationInfo{`0}\)), y se crea una instancia de la clase [ShardLocation](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardlocation.shardlocation.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardLocation.).</span><span class="sxs-lookup"><span data-stu-id="aa146-109">This sample uses the [TryGetShard](https://msdn.microsoft.com/library/azure/dn823929.aspx) the [CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx), [CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn807221.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeShardMap`1.CreateRangeMapping\(Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeMappingCreationInfo{`0}\)) methods, and creates an instance of the [ShardLocation](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardlocation.shardlocation.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardLocation.) class.</span></span> <span data-ttu-id="aa146-110">En el ejemplo siguiente, se ha creado una base de datos denominada **sample_shard_2** y todos los objetos de esquema necesarios en su interior para contener el intervalo [300, 400).</span><span class="sxs-lookup"><span data-stu-id="aa146-110">In the sample below, a database named **sample_shard_2** and all necessary schema objects inside of it have been created to hold range [300, 400).</span></span>  

    // sm is a RangeShardMap object.
    // Add a new shard to hold the range being added. 
    Shard shard2 = null; 

    if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
    { 
        shard2 = sm.CreateShard(new ShardLocation(shardServer, "sample_shard_2"));  
    } 

    // Create the mapping and associate it with the new shard 
    sm.CreateRangeMapping(new RangeMappingCreationInfo<long> 
                            (new Range<long>(300, 400), shard2, MappingStatus.Online)); 


<span data-ttu-id="aa146-111">Como alternativa, puede usar Powershell para crear un nuevo Administrador de mapas de particiones.</span><span class="sxs-lookup"><span data-stu-id="aa146-111">As an alternative, you can use Powershell to create a new Shard Map Manager.</span></span> <span data-ttu-id="aa146-112">Hay un ejemplo disponible [aquí](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="aa146-112">An example is available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

## <a name="to-add-a-shard-for-an-empty-part-of-an-existing-range"></a><span data-ttu-id="aa146-113">Para agregar una partición para un área vacía de un intervalo existente</span><span class="sxs-lookup"><span data-stu-id="aa146-113">To add a shard for an empty part of an existing range</span></span>
<span data-ttu-id="aa146-114">En algunas circunstancias, tiene ya asignado un intervalo a una partición y se rellena parcialmente con datos, pero ahora desea que los próximos datos se dirijan a una partición diferente.</span><span class="sxs-lookup"><span data-stu-id="aa146-114">In some circumstances, you may have already mapped a range to a shard and partially filled it with data, but you now want upcoming data to be directed to a different shard.</span></span> <span data-ttu-id="aa146-115">Por ejemplo, realiza particiones por intervalo de días y ya ha asignado 50 días a una partición, pero en el día 24 decide que desea que los datos futuros lleguen a una partición diferente.</span><span class="sxs-lookup"><span data-stu-id="aa146-115">For example, you shard by day range and have already allocated 50 days to a shard, but on day 24, you want future data to land in a different shard.</span></span> <span data-ttu-id="aa146-116">La [herramienta de división y combinación](sql-database-elastic-scale-overview-split-and-merge.md) de la base de datos elástica puede realizar esta operación, pero si el movimiento de datos no es necesario (por ejemplo, los datos para el intervalo de días [25, 50), es decir, desde el día 25 inclusive hasta el 50 exclusive, aún no existen) es posible realizar esta operación por completo utilizando directamente las API de administración de mapas de particiones.</span><span class="sxs-lookup"><span data-stu-id="aa146-116">The elastic database [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md) can perform this operation, but if data movement is not necessary (for example, data for the range of days [25, 50), i.e., day 25 inclusive to 50 exclusive, does not yet exist) you can perform this entirely using the Shard Map Management APIs directly.</span></span>

### <a name="example-splitting-a-range-and-assigning-the-empty-portion-to-a-newly-added-shard"></a><span data-ttu-id="aa146-117">Ejemplo: división de un intervalo y asignación de la parte vacía a una partición recién agregada</span><span class="sxs-lookup"><span data-stu-id="aa146-117">Example: splitting a range and assigning the empty portion to a newly-added shard</span></span>
<span data-ttu-id="aa146-118">Se ha creado una base de datos denominada "sample_shard_2" y todos los objetos de esquema necesarios en su interior.</span><span class="sxs-lookup"><span data-stu-id="aa146-118">A database named “sample_shard_2” and all necessary schema objects inside of it have been created.</span></span>  

    // sm is a RangeShardMap object.
    // Add a new shard to hold the range we will move 
    Shard shard2 = null; 

    if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
    { 

        shard2 = sm.CreateShard(new ShardLocation(shardServer, "sample_shard_2"));  
    } 

    // Split the Range holding Key 25 

    sm.SplitMapping(sm.GetMappingForKey(25), 25); 

    // Map new range holding [25-50) to different shard: 
    // first take existing mapping offline 
    sm.MarkMappingOffline(sm.GetMappingForKey(25)); 
    // now map while offline to a different shard and take online 
    RangeMappingUpdate upd = new RangeMappingUpdate(); 
    upd.Shard = shard2; 
    sm.MarkMappingOnline(sm.UpdateMapping(sm.GetMappingForKey(25), upd)); 

<span data-ttu-id="aa146-119">**Importante**: Use esta técnica solo si está seguro de que el intervalo para la asignación actualizada está vacío.</span><span class="sxs-lookup"><span data-stu-id="aa146-119">**Important**:  Use this technique only if you are certain that the range for the updated mapping is empty.</span></span>  <span data-ttu-id="aa146-120">Los métodos anteriores no comprueban los datos para el intervalo que se va a mover, por lo que es mejor incluir comprobaciones en el código.</span><span class="sxs-lookup"><span data-stu-id="aa146-120">The methods above do not check data for the range being moved, so it is best to include checks in your code.</span></span>  <span data-ttu-id="aa146-121">Si existen filas en el intervalo que se va a mover, la distribución de datos real no coincidirá con el mapa de particiones actualizado.</span><span class="sxs-lookup"><span data-stu-id="aa146-121">If rows exist in the range being moved, the actual data distribution will not match the updated shard map.</span></span> <span data-ttu-id="aa146-122">Use la [herramienta de división y combinación](sql-database-elastic-scale-overview-split-and-merge.md) para realizar la operación en su lugar en estos casos.</span><span class="sxs-lookup"><span data-stu-id="aa146-122">Use the [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md) to perform the operation instead in these cases.</span></span>  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

