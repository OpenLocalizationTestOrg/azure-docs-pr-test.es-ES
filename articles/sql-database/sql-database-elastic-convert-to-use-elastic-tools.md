---
title: aaaMigrate existente bases de datos fuera de tooscale | Documentos de Microsoft
description: "Convertir herramientas de bases de datos particionadas toouse elástico de base de datos mediante la creación de un administrador de mapa de particiones"
services: sql-database
documentationcenter: 
author: ddove
manager: jhubbard
editor: 
ms.assetid: 8c851d8e-8fd5-4327-89c1-9178b20ddd69
ms.service: sql-database
ms.custom: scale out apps
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: fa2c9e3699f30667cf547d1faadf4504609199be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-existing-databases-tooscale-out"></a>Migrar tooscale-fuera de las bases de datos existente
Administrar fácilmente la capacidad de ampliación horizontal particionadas bases de datos existentes con herramientas de base de datos de base de datos de SQL Azure (por ejemplo, hello [biblioteca de cliente de base de datos elástica](sql-database-elastic-database-client-library.md)). Primero debe convertir un conjunto existente de Hola de bases de datos toouse [manager de mapa de particiones](sql-database-elastic-scale-shard-map-management.md). 

## <a name="overview"></a>Información general
toomigrate una base de datos particionada existente: 

1. Preparar hello [base de datos de administrador de asignación de particiones](sql-database-elastic-scale-shard-map-management.md).
2. Crear mapa de particiones de Hola.
3. Preparar las particiones individuales Hola.  
4. Agregue el mapa de particiones de toohello de asignaciones.

Estas técnicas se pueden implementar con cualquier hello [biblioteca de cliente de .NET Framework](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/), o los scripts de PowerShell de Hola se encuentran en [base de datos de SQL de Azure: secuencias de comandos de herramientas de base de datos elástica](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db). ejemplos de Hello aquí usan scripts de PowerShell de Hola.

Para obtener más información acerca de hello ShardMapManager, consulte [administración de mapa de particiones](sql-database-elastic-scale-shard-map-management.md). Para obtener información general de herramientas de base de datos elástica hello, consulte [Introducción a características de base de datos elástica](sql-database-elastic-scale-introduction.md).

## <a name="prepare-hello-shard-map-manager-database"></a>Preparar base de datos de administrador de asignación de hello particiones
el Administrador de mapa de particiones de Hello es una base de datos especial que contiene las bases de datos de escala horizontal de hello datos toomanage. Puede utilizar una base de datos existente o crear una nueva. Tenga en cuenta que una base de datos que actúa como administrador de asignación de partición no debe ser Hola misma base de datos como una partición. Tenga en cuenta también que script de PowerShell de hello no crear base de datos de Hola para usted. 

## <a name="step-1-create-a-shard-map-manager"></a>Paso 1: crear un administrador de mapas de particiones
    # Create a shard map manager. 
    New-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 
    #<server_name> and <smm_db_name> are hello server name and database name 
    # for hello new or existing database that should be used for storing 
    # tenant-database mapping information.

### <a name="tooretrieve-hello-shard-map-manager"></a>Administrador de mapa de particiones de hello tooretrieve
Después de la creación, puede recuperar el Administrador de mapa de particiones de hello con este cmdlet. Este paso es necesario cada vez que se necesita toouse hello ShardMapManager objeto.

    # Try tooget a reference toohello Shard Map Manager  
    $ShardMapManager = Get-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 


## <a name="step-2-create-hello-shard-map"></a>Paso 2: crear el mapa de particiones de Hola
Debe seleccionar tipo de Hola de toocreate de mapa de particiones. elección de Hello depende de la arquitectura de base de datos de hello: 

1. Un inquilino por base de datos (para obtener términos, vea hello [glosario](sql-database-elastic-scale-glossary.md).) 
2. Varios inquilinos por base de datos (dos tipos):
   1. Asignación de lista
   2. Asignación de intervalo

Para un modelo de un solo inquilino, cree un mapa de particiones de **asignación de lista** . modelo de Hello único inquilino asigna una base de datos por inquilino. Se trata de un modelo eficaz para desarrolladores de SaaS, pues simplifica la administración.

![Asignación de lista][1]

modelo de varios inquilinos de Hello asigna a varios inquilinos tooa única base de datos (y grupos de inquilinos puede distribuir a través de varias bases de datos). Use este modelo cuando espera que necesitan cada datos pequeños de toohave de inquilino. En este modelo, se asigna un intervalo de los inquilinos tooa base de datos usando **asignación de intervalo**. 

![Asignación de intervalo][2]

O puede implementar un modelo de base de datos de varios inquilinos mediante un *asignación de lista* tooassign varios inquilinos tooa única base de datos. Por ejemplo, DB1 es toostore usa información acerca del Id. de inquilino 1 y 5, y DB2 almacena los datos de inquilino 10 e inquilino 7. 

![Varios inquilinos en una sola base de datos][3] 

**En función de su elección, elija una de estas opciones:**

### <a name="option-1-create-a-shard-map-for-a-list-mapping"></a>Opción 1: crear un mapa de particiones para una asignación de lista
Crear un mapa de particiones con objeto de ShardMapManager Hola. 

    # $ShardMapManager is hello shard map manager object. 
    $ShardMap = New-ListShardMap -KeyType $([int]) 
    -ListShardMapName 'ListShardMap' 
    -ShardMapManager $ShardMapManager 


### <a name="option-2-create-a-shard-map-for-a-range-mapping"></a>Opción 2: crear un mapa de particiones para una asignación de intervalo
Tenga en cuenta que tooutilize este patrón de asignación, los valores de Id. de inquilino debe toobe continua intervalos y es espacio toohave aceptable en intervalos de hello simplemente omitiendo intervalo Hola al crear las bases de datos de Hola.

    # $ShardMapManager is hello shard map manager object 
    # 'RangeShardMap' is hello unique identifier for hello range shard map.  
    $ShardMap = New-RangeShardMap 
    -KeyType $([int]) 
    -RangeShardMapName 'RangeShardMap' 
    -ShardMapManager $ShardMapManager 

### <a name="option-3-list-mappings-on-a-single-database"></a>Opción 3: asignaciones de lista en una base de datos única
La configuración de este patrón también requiere la creación de un mapa de lista, tal como se muestra en el paso 2, opción 1.

## <a name="step-3-prepare-individual-shards"></a>Paso 3: preparar particiones individuales
Agregue cada administrador de mapa de particiones (base de datos) toohello particiones. Esto prepara las bases de datos individuales de Hola para almacenar información de asignación. Ejecute este método en cada partición.

    Add-Shard 
    -ShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>'
    # hello $ShardMap is hello shard map created in step 2.


## <a name="step-4-add-mappings"></a>Paso 4: agregar asignaciones
Adición de Hola de asignaciones depende de tipo hello de mapa de particiones que ha creado. Si ha creado un mapa de lista, agregue asignaciones de lista. Si ha creado un mapa de intervalo, agregue asignaciones de intervalo.

### <a name="option-1-map-hello-data-for-a-list-mapping"></a>Opción 1: asignar datos de Hola para una asignación de lista
Asignar datos de hello mediante la adición de una asignación de lista para cada inquilino.  

    # Create hello mappings and associate it with hello new shards 
    Add-ListMapping 
    -KeyType $([int]) 
    -ListPoint '<tenant_id>' 
    -ListShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 

### <a name="option-2-map-hello-data-for-a-range-mapping"></a>Opción 2: asignar datos de Hola para una asignación de intervalo
Agregar asignaciones de intervalo de Hola para todos los Hola inquilino intervalo de Id. - las asociaciones de la base de datos:

    # Create hello mappings and associate it with hello new shards 
    Add-RangeMapping 
    -KeyType $([int]) 
    -RangeHigh '5' 
    -RangeLow '1' 
    -RangeShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 


### <a name="step-4-option-3-map-hello-data-for-multiple-tenants-on-a-single-database"></a>Paso 4 opción 3: asignar datos de Hola para varios inquilinos en una sola base de datos
Para cada inquilino, ejecute hello ListMapping agregar (opción 1, anteriormente). 

## <a name="checking-hello-mappings"></a>Comprobación de asignaciones de Hola
Puede consultar información acerca de las particiones existentes hello y asignaciones de hello asociadas a ellos con los siguientes comandos:  

    # List hello shards and mappings 
    Get-Shards -ShardMap $ShardMap 
    Get-Mappings -ShardMap $ShardMap 

## <a name="summary"></a>Resumen
Una vez haya completado el programa de instalación de hello, puede empezar a biblioteca de cliente de base de datos elástica toouse Hola. También puede usar las características de [enrutamiento dependiente de los datos](sql-database-elastic-scale-data-dependent-routing.md) y [consulta a través de particiones múltiples](sql-database-elastic-scale-multishard-querying.md).

## <a name="next-steps"></a>Pasos siguientes
Obtener scripts de PowerShell de Hola de [sripts de herramientas de base de datos de Azure SQL DB elásticas](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).

herramientas de Hello también están en GitHub: [Azure/elásticas-db-tools](https://github.com/Azure/elastic-db-tools).

Utilice Hola herramienta Dividir-combinar toomove datos tooor de un modelo de un solo inquilino de tooa de modelo de varios inquilinos. Consulte el artículo sobre la [herramienta de división y combinación](sql-database-elastic-scale-get-started.md).

## <a name="additional-resources"></a>Recursos adicionales
Para obtener información sobre los patrones comunes de la arquitectura de datos de aplicaciones de base de datos de software como servicio (SaaS) multiinquilino, consulte [Modelos de diseño para las aplicaciones SaaS multiinquilino con base de datos SQL de Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md).

## <a name="questions-and-feature-requests"></a>Preguntas y solicitudes de características
Si tiene preguntas, póngase en contacto toous en hello [foro de base de datos SQL](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) y para las solicitudes de características, agréguelos toohello [foro de comentarios de la base de datos SQL](https://feedback.azure.com/forums/217321-sql-database/).

<!--Image references-->
[1]: ./media/sql-database-elastic-convert-to-use-elastic-tools/listmapping.png
[2]: ./media/sql-database-elastic-convert-to-use-elastic-tools/rangemapping.png
[3]: ./media/sql-database-elastic-convert-to-use-elastic-tools/multipleonsingledb.png

