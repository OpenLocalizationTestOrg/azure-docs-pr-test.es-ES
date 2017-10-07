---
title: bases de datos de SQL Azure particionadas aaaQuery | Documentos de Microsoft
description: "Ejecutar consultas entre particiones mediante la biblioteca de cliente de base de datos elástica Hola."
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
editor: 
ms.assetid: a4379c15-f213-4026-ab6f-a450ee9d5758
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2016
ms.author: torsteng
ms.openlocfilehash: a1f0763935a6807b74aa9dec477714e8d117417d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="multi-shard-querying"></a>Consultas a través de particiones múltiples
## <a name="overview"></a>Información general
Con hello [herramientas de base de datos elástica](sql-database-elastic-scale-introduction.md), puede crear soluciones de base de datos particionada. **Consultas a través de particiones múltiples** se usa para tareas como informes y recopilación de datos que requieren ejecutar una consulta que abarca varias particiones. (Esto contrasta demasiado[enrutamiento dependiente de los datos](sql-database-elastic-scale-data-dependent-routing.md), que realiza todo el trabajo en una sola partición.) 

1. Obtener un [ **RangeShardMap** ](https://msdn.microsoft.com/library/azure/dn807318.aspx) o [ **ListShardMap** ](https://msdn.microsoft.com/library/azure/dn807370.aspx) con hello [ **TryGetRangeShardMap** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), hello [ **TryGetListShardMap**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), o hello [ **GetShardMap** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) método. Consulte [**Construcción de un ShardMapManager**](sql-database-elastic-scale-shard-map-management.md#constructing-a-shardmapmanager) y [**Obtención de las clases RangeShardMap o ListShardMap**](sql-database-elastic-scale-shard-map-management.md#get-a-rangeshardmap-or-listshardmap).
2. Cree un objeto **[MultiShardConnection](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardconnection.aspx)**.
3. Cree un objeto **[MultiShardCommand](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.aspx)**. 
4. Conjunto hello  **[propiedad CommandText](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.commandtext.aspx#P:Microsoft.Azure.SqlDatabase.ElasticScale.Query.MultiShardCommand.CommandText)**  tooa comando T-SQL.
5. Ejecutar comando de Hola Hola llamada  **[método ExecuteReader](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.executereader.aspx)**.
6. Ver los resultados de hello mediante hello  **[MultiShardDataReader clase](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multisharddatareader.aspx)**. 

## <a name="example"></a>Ejemplo
Hello código siguiente muestra el uso de Hola de varias particiones realizar consultas con un determinado **ShardMap** denominado *myShardMap*. 

    using (MultiShardConnection conn = new MultiShardConnection( 
                                        myShardMap.GetShards(), 
                                        myShardConnectionString) 
          ) 
    { 
    using (MultiShardCommand cmd = conn.CreateCommand())
           { 
            cmd.CommandText = "SELECT c1, c2, c3 FROM ShardedTable"; 
            cmd.CommandType = CommandType.Text; 
            cmd.ExecutionOptions = MultiShardExecutionOptions.IncludeShardNameColumn; 
            cmd.ExecutionPolicy = MultiShardExecutionPolicy.PartialResults; 

            using (MultiShardDataReader sdr = cmd.ExecuteReader()) 
                { 
                    while (sdr.Read())
                        { 
                            var c1Field = sdr.GetString(0); 
                            var c2Field = sdr.GetFieldValue<int>(1); 
                            var c3Field = sdr.GetFieldValue<Int64>(2);
                        } 
                 } 
           } 
    } 


Una diferencia fundamental es la construcción de Hola de conexiones de varias particiones. Donde **SqlConnection** funciona en una sola base de datos, hello **MultiShardConnection** toma una ***colección de particiones*** como entrada. Rellenar la colección de Hola de particiones de un mapa de particiones. a continuación, se ejecuta la consulta de Hello en la colección de Hola de particiones con **UNION ALL** semántica tooassemble un único resultado total. Si lo desea, puede agregarse a nombre Hola de particiones de Hola donde se origina la fila de hello toohello Hola de salida **ExecutionOptions** propiedad en el comando. 

Tenga en cuenta llamada Hola demasiado**myShardMap.GetShards()**. Este método recupera todas las particiones de mapa de particiones de Hola y proporciona una manera sencilla de toorun una consulta en todas las bases de datos relevantes. Hello colección de particiones para una consulta de varias particiones se puede refinar aún más realizando una LINQ consultar sobre colección de hello devuelta de la llamada de hello demasiado**myShardMap.GetShards()**. En combinación con la directiva de resultados parciales de hello, capacidad de corriente de hello en varias particiones consultar ha sido diseñada toowork bien para decenas seguridad toohundreds de particiones.

Una limitación con particiones múltiples consultas actualmente es falta de Hola de validación de particiones y shardlets que se consultan. Mientras que enrutamiento dependiente de los datos, se comprueba que una partición determinada es parte del mapa de particiones de hello en tiempo de presentación de las consultas, las consultas de varias particiones no realizar esta comprobación. Esto puede provocar que las consultas de toomulti particiones que se ejecutan en bases de datos que se han quitado de mapa de particiones de Hola.

## <a name="multi-shard-queries-and-split-merge-operations"></a>Consultas a través de particiones múltiples y operaciones de división y combinación
Las consultas de varias particiones no comprueban si shardlets en la base de datos consultados de hello forman parte de las operaciones de división de combinación en curso. (Consulte [escalado mediante la herramienta Hola bases de datos elásticas dividir-combinar](sql-database-elastic-scale-overview-split-and-merge.md).) Esto puede provocar tooinconsistencies donde filas de Hola misma presentación de shardlet para varias bases de datos en hello misma consulta de varias particiones. Tenga en cuenta estas limitaciones y considere la posibilidad de purgar en curso dividir-combinar cambios y operaciones toohello mapa de particiones al realizar consultas de varias particiones.

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

## <a name="see-also"></a>Otras referencias
Clases y métodos **[System.Data.SqlClient](http://msdn.microsoft.com/library/System.Data.SqlClient.aspx)**.

Administrar particiones con hello [biblioteca de cliente de base de datos elástica](sql-database-elastic-database-client-library.md). Incluye un espacio de nombres denominado [Microsoft.Azure.SqlDatabase.ElasticScale.Query](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.aspx) que proporciona Hola capacidad tooquery varias particiones con una sola consulta y resultado. Brinda una abstracción de consulta sobre una recopilación de particiones. También proporciona las directivas de ejecución alternativo, los resultados parciales en particular, toodeal con errores cuando las consultas en varias particiones.  

