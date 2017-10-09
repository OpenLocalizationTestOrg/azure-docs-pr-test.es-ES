---
title: contadores de aaaPerformance para el Administrador de mapa de particiones
description: Clase ShardMapManager y contadores de rendimiento de enrutamiento dependiente de los datos
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: b090aba0-2e30-454c-96b3-dffa281f539a
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: ddove
ms.openlocfilehash: d24198563d9fa88d12e6c464dbe89bc300e72ca0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="performance-counters-for-shard-map-manager"></a>Contadores de rendimiento para Shard Map Manager
Puede capturar Hola de rendimiento de un [manager de mapa de particiones](sql-database-elastic-scale-shard-map-management.md), especialmente cuando se usa [enrutamiento dependiente de datos](sql-database-elastic-scale-data-dependent-routing.md). Los contadores se crean con métodos de hello Microsoft.Azure.SqlDatabase.ElasticScale.Client clase.  

Contadores son utilizados tootrack Hola rendimiento de [enrutamiento dependiente de datos](sql-database-elastic-scale-data-dependent-routing.md) operaciones. Estos contadores son accesibles en hello Monitor de rendimiento, en la categoría de "Administración de particiones de elástico bases de datos:" ¡hello.

**Para la versión más reciente de hello:** vaya demasiado[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/). Vea también [actualizar una aplicación toouse hello más reciente bases de datos elásticas bibliotecas de cliente](sql-database-elastic-scale-upgrade-client-library.md).

## <a name="prerequisites"></a>Requisitos previos
* Hola toocreate la categoría de rendimiento de Hola y contadores de usuario debe formar parte de hello local **administradores** grupo máquina Hola hospeda aplicación Hola.  
* instancia de contador de toocreate un rendimiento y actualizar los contadores de hello, Hola usuario debe ser un miembro de cualquier hello **administradores** o **usuarios del Monitor de rendimiento** grupo. 

## <a name="create-performance-category-and-counters"></a>Creación de la categoría y los contadores de rendimiento
contadores de hello toocreate, llame al método de CreatePeformanceCategoryAndCounters de Hola de hello [ShardMapManagmentFactory clase](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx). Sólo un administrador puede ejecutar el método hello: 

    ShardMapManagerFactory.CreatePerformanceCategoryAndCounters()  

También puede usar [esto](https://gallery.technet.microsoft.com/scriptcenter/Elastic-DB-Tools-for-Azure-17e3d283) método de hello tooexecute de script de PowerShell. método Hello crea Hola siguiendo los contadores de rendimiento:  

* **Almacena en caché las asignaciones**: número de asignaciones que se almacenan en caché para el mapa de particiones de Hola.
* **DDR operaciones/seg**: tasa de operaciones de enrutamiento dependiente de datos de mapa de particiones de Hola. Este contador se actualiza cuando una llamada demasiado[OpenConnectionForKey()](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx) da como resultado una partición de destino toohello de conexión correcta. 
* **Asignación de búsqueda de aciertos de caché/s**: tasa de operaciones de búsqueda de caché correcta para las asignaciones en el mapa de particiones de Hola. 
* **Asignación de búsqueda de errores de caché/seg.**: tasa de operaciones de búsqueda de errores de caché para las asignaciones en el mapa de particiones de Hola.
* **Asignaciones de agregado o actualizado en la caché/s**: ritmo al que se van a agregar las asignaciones o actualizado en caché para el mapa de particiones de Hola. 
* **Quitaron las asignaciones desde la caché/s**: tasa a la que se quitan los asignaciones de memoria caché de mapa de particiones de Hola. 

Los contadores de rendimiento se crean para cada mapa de particiones en caché por proceso.  

## <a name="notes"></a>Notas
Hello siguientes eventos desencadenan la creación de Hola Hola de contadores de rendimiento:  

* Inicialización de hello [ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) con [carga diligente](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerloadpolicy.aspx), si hello ShardMapManager contiene las asignaciones de particiones. Puede tratarse de hello [GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx?f=255&MSPPError=-2147217396#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardMapManagerFactory.GetSqlShardMapManager%28System.String,Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardMapManagerLoadPolicy%29) hello y [TryGetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx) métodos.
* Búsqueda correcta de un mapa de particiones (mediante [GetShardMap()](https://msdn.microsoft.com/library/azure/dn824215.aspx), [GetListShardMap()](https://msdn.microsoft.com/library/azure/dn824212.aspx) o [GetRangeShardMap()](https://msdn.microsoft.com/library/azure/dn824173.aspx)). 
* Creación correcta de un mapa de particiones con CreateShardMap().

contadores de rendimiento de Hola se actualizará por todas las operaciones de caché que se realiza en las asignaciones y mapa de particiones de Hola. Eliminación correcta del mapa de particiones de hello mediante DeleteShardMap () reults de eliminación de esta instancia de contadores de rendimiento de Hola.  

## <a name="best-practices"></a>Prácticas recomendadas
* Creación de la categoría de rendimiento de Hola y contadores debe realizarse una sola vez antes de la creación de hello del objeto ShardMapManager. Cada ejecución del comando de hello CreatePerformanceCategoryAndCounters() borra contadores anterior hello (perder los datos notificados por todas las instancias) y crea otras nuevas.  
* Las instancias de contadores de rendimiento se crean por proceso. Cualquier bloqueo de aplicación o la eliminación de un mapa de particiones de memoria caché de hello dará como resultado una eliminación de instancias de contadores de rendimiento de Hola.  

### <a name="see-also"></a>Otras referencias
[Información general de las características de bases de datos elásticas](sql-database-elastic-scale-introduction.md)  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->

