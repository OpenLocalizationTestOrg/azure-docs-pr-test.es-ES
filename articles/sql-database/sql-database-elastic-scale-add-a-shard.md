---
title: "aaaAdding una partición con herramientas de base de datos elástica | Documentos de Microsoft"
description: "Cómo establece toouse API de escala elástica tooadd nueva particiones tooa partición."
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
ms.openlocfilehash: f44b59578376d1238b3012a3cb52339978079f0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="adding-a-shard-using-elastic-database-tools"></a>Incorporación de una partición con herramientas de bases de datos elásticas
## <a name="tooadd-a-shard-for-a-new-range-or-key"></a>tooadd una partición para un nuevo intervalo o clave
Las aplicaciones a menudo necesita toosimply agregar nuevos datos de toohandle de particiones que cabe esperar de nuevas claves o intervalos de claves de un mapa de particiones que ya existe. Por ejemplo, una aplicación particionada por Id. de inquilino puede necesitar tooprovision una nueva partición para un nuevo inquilino o mensual de particiones de datos que necesite una nueva partición aprovisionada antes del inicio de Hola de nuevo cada mes. 

Si el nuevo intervalo de valores de clave de hello ya no forma parte de una asignación existente, es tooadd muy sencillo Hola nueva partición y asociar Hola nueva clave o intervalo toothat partición. 

### <a name="example--adding-a-shard-and-its-range-tooan-existing-shard-map"></a>Ejemplo: agregar una partición y su mapa de particiones de intervalo tooan existente
Este ejemplo utiliza hello [TryGetShard](https://msdn.microsoft.com/library/azure/dn823929.aspx) hello [CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx), [CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn807221.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeShardMap`1.CreateRangeMapping\(Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeMappingCreationInfo{`0}\)) métodos y crea una instancia de hello [ShardLocation](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardlocation.shardlocation.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardLocation.) clase. En el ejemplo de Hola a continuación, una base de datos denominada **sample_shard_2** y todos los objetos de esquema necesarios en su interior se han creado el intervalo de toohold [300, 400).  

    // sm is a RangeShardMap object.
    // Add a new shard toohold hello range being added. 
    Shard shard2 = null; 

    if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
    { 
        shard2 = sm.CreateShard(new ShardLocation(shardServer, "sample_shard_2"));  
    } 

    // Create hello mapping and associate it with hello new shard 
    sm.CreateRangeMapping(new RangeMappingCreationInfo<long> 
                            (new Range<long>(300, 400), shard2, MappingStatus.Online)); 


Como alternativa, puede usar Powershell toocreate un nuevo administrador de mapa de particiones. Hay un ejemplo disponible [aquí](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).

## <a name="tooadd-a-shard-for-an-empty-part-of-an-existing-range"></a>tooadd una partición para una parte vacía de un rango existente
En algunas circunstancias, se pueden tener ya asignado a una partición de tooa de intervalo y parcialmente se rellena con datos, pero ahora desea que diferentes particiones de datos de las próximas toobe tooa dirigido. Por ejemplo, se particiones por día de intervalo y ya se ha asignado la partición de tooa 50 días, pero en el día 24, desea tooland de datos en el futuro en una partición diferente. base de datos elástica Hello [herramienta Dividir-combinar](sql-database-elastic-scale-overview-split-and-merge.md) pueden realizar esta operación, pero si el movimiento de datos no es necesario (por ejemplo, datos de duración de Hola de días [25, 50), es decir, día 25 inclusivo too50 exclusivo, aún no existe) se pueden realizar Este por completo mediante Hola directamente a las API de administración de mapa de particiones.

### <a name="example-splitting-a-range-and-assigning-hello-empty-portion-tooa-newly-added-shard"></a>Ejemplo: dividir un intervalo y asignar Hola vacía partición recién agregado de parte tooa
Se ha creado una base de datos denominada "sample_shard_2" y todos los objetos de esquema necesarios en su interior.  

    // sm is a RangeShardMap object.
    // Add a new shard toohold hello range we will move 
    Shard shard2 = null; 

    if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
    { 

        shard2 = sm.CreateShard(new ShardLocation(shardServer, "sample_shard_2"));  
    } 

    // Split hello Range holding Key 25 

    sm.SplitMapping(sm.GetMappingForKey(25), 25); 

    // Map new range holding [25-50) toodifferent shard: 
    // first take existing mapping offline 
    sm.MarkMappingOffline(sm.GetMappingForKey(25)); 
    // now map while offline tooa different shard and take online 
    RangeMappingUpdate upd = new RangeMappingUpdate(); 
    upd.Shard = shard2; 
    sm.MarkMappingOnline(sm.UpdateMapping(sm.GetMappingForKey(25), upd)); 

**Importante**: Use esta técnica solo si está seguro de que Hola intervalo de asignación de hello actualizado está vacío.  métodos de Hello anteriores no comprobar los datos para que se va a mover el intervalo de hello, por lo que es mejor tooinclude comprueba en el código.  Si existen filas en que se mueven de intervalo de hello, distribución de datos reales de hello no coincidirán mapa de particiones actualizada de Hola. Hola de uso [herramienta Dividir-combinar](sql-database-elastic-scale-overview-split-and-merge.md) tooperform Hola operación en su lugar en estos casos.  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

