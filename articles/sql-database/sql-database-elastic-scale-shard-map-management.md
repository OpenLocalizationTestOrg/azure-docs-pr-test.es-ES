---
title: aaaScale una base de datos SQL de Azure | Documentos de Microsoft
description: "¿Cómo toouse Hola ShardMapManager, biblioteca de cliente de base de datos elástica"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 0e9d647a-9ba9-4875-aa22-662d01283439
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 4cf670d42ad7ded98fb8d6f0830154587dd2c6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scale-out-databases-with-hello-shard-map-manager"></a>Escalar horizontalmente bases de datos con el Administrador de mapa de particiones de Hola
tooeasily escalada bases de datos de SQL Azure, utilice un administrador de mapa de particiones. el Administrador de mapa de particiones de Hello es una base de datos especial que mantiene la información de asignación global acerca de todas las particiones (bases de datos) en un conjunto de particiones. Hola de metadatos permite a una aplicación tooconnect toohello base de datos correcta en función de valor de Hola de hello **clave de particionamiento**. Además, cada partición en conjunto hello contiene asignaciones que realizan el seguimiento de datos de la partición local de hello (conocido como **shardlets**). 

![Administración de mapas de particiones.](./media/sql-database-elastic-scale-shard-map-management/glossary.png)

Descripción de cómo se construyen estas asignaciones es esencial tooshard de administración de mapa. Esto se realiza mediante hello [ShardMapManager clase](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx), que se encuentra en hello [biblioteca de cliente de base de datos elástica](sql-database-elastic-database-client-library.md) toomanage partición se asigna.  

## <a name="shard-maps-and-shard-mappings"></a>Mapas de particiones y asignaciones de particiones
Para cada partición, debe seleccionar tipo de Hola de toocreate de mapa de particiones. elección de Hello depende de la arquitectura de base de datos de hello: 

1. Un solo inquilino por base de datos  
2. Varios inquilinos por base de datos (dos tipos):
   1. Asignación de lista
   2. Asignación de intervalo

Para un modelo de un solo inquilino, cree un mapa de particiones de **asignación de lista** . modelo de Hello único inquilino asigna una base de datos por inquilino. Se trata de un modelo eficaz para desarrolladores de SaaS, pues simplifica la administración.

![Asignación de lista][1]

modelo de varios inquilinos de Hello asigna a varios inquilinos tooa única base de datos (y grupos de inquilinos puede distribuir a través de varias bases de datos). Use este modelo cuando espera que necesitan cada datos pequeños de toohave de inquilino. En este modelo, se asigna un intervalo de los inquilinos tooa base de datos usando **asignación de intervalo**. 

![Asignación de intervalo][2]

O puede implementar un modelo de base de datos de varios inquilinos mediante un *asignación de lista* tooassign varios inquilinos tooa única base de datos. Por ejemplo, DB1 es toostore usa información acerca del Id. de inquilino 1 y 5, y DB2 almacena los datos de inquilino 10 e inquilino 7. 

![Varios inquilinos en una sola base de datos][3] 

### <a name="supported-net-types-for-sharding-keys"></a>Tipos .NET admitidos para claves de particionamiento
Hola de soporte técnico de escala elástica después de .net Framework los tipos como claves de particionamiento:

* integer
* long
* guid
* byte[]  
* datetime
* timespan
* datetimeoffset

### <a name="list-and-range-shard-maps"></a>Mapas de particiones de lista y de intervalo
Los mapas de particiones se pueden construir mediante **listas de valores individuales de clave de particionamiento**, o por medio de **intervalos de valores de clave de particionamiento**. 

### <a name="list-shard-maps"></a>Mapas de particiones de lista
**Particiones** contienen **shardlets** y asignación de Hola de shardlets tooshards se mantiene un mapa de particiones. A **mapa de particiones de lista** es una asociación entre los valores clave individuales Hola que identifican hello shardlets y bases de datos de Hola que actúan como particiones.  **Enumerar asignaciones** explícitas y distintos valores de clave pueden ser asignado toohello misma base de datos. Por ejemplo, la clave 1 asigna tooDatabase A y B. de base de datos hacen referencia a valores de clave 3 y 6

| Clave | Ubicación de la partición |
| --- | --- |
| 1 |Database_A |
| 3 |Database_B |
| 4 |Database_C |
| 6 |Database_B |
| ... |... |

### <a name="range-shard-maps"></a>Mapas de particiones de intervalo
En un **mapa de particiones de intervalo**, intervalo de claves de Hola se describe mediante un par **[valor bajo, alto valor)** donde Hola *bajo valor* es clave mínimo de hello en el intervalo de Hola y Hola *Valor alto* es Hola primer valor mayor que el intervalo de saludo. 

Por ejemplo **[0, 100)** incluye todos los números enteros que son mayores o iguales que 0 y menores que 100. Tenga en cuenta que se admiten varios intervalos can punto toohello misma base de datos y discontinuas intervalos (por ejemplo, [100,200) y [400,600) ambos tooDatabase punto C en el siguiente ejemplo de Hola.)

| Clave | Ubicación de la partición |
| --- | --- |
| [1,50) |Database_A |
| [50,100) |Database_B |
| [100,200) |Database_C |
| [400,600) |Database_C |
| ... |... |

Cada una de las tablas de hello mostradas anteriormente es un ejemplo conceptual de un **ShardMap** objeto. Cada fila es un ejemplo simplificado de una persona **PointMapping** (para el mapa de particiones de la lista de hello) o **RangeMapping** (para el mapa de particiones de intervalo de hello) objetos.

## <a name="shard-map-manager"></a>Administrador de mapas de particiones
En la biblioteca de cliente de Hola, Administrador de mapa de particiones de hello es una colección de asignaciones de particiones. Hola datos administrados por un **ShardMapManager** instancia se mantiene en tres lugares: 

1. **Mapa de particiones global (GSM)**: especificar un tooserve de base de datos como repositorio de Hola para todos sus asignaciones de particiones y asignaciones. Tablas especiales y los procedimientos almacenados se crean automáticamente información de hello toomanage. Esto suele ser una pequeña base de datos y con menos acceso, y no debe usarse para otras necesidades de la aplicación hello. Hello tablas están en un esquema especial llamado **__ShardManagement**. 
2. **Mapa de particiones locales (LSM)**: cada base de datos que especifique toobe una partición es modifica toocontain varias tablas pequeñas y los procedimientos almacenados especiales que contienen y administración particiones de toothat específico de información de mapa de particiones. Esta información es redundante con información de Hola Hola GSM y permite información de la asignación de particiones de hello aplicación toovalidate almacenado en memoria caché sin incluir ninguna carga en hello GSM; aplicación Hello usa Hola LSM toodetermine si una asignación almacenada en caché sigue siendo válida. Hola tablas correspondiente toohello LSM en cada partición también están en el esquema de hello **__ShardManagement**.
3. **Caché de aplicación**: cada instancia de la aplicación que accede a un objeto **ShardMapManager** mantiene una caché en memoria local de sus asignaciones. Almacena información de enrutamiento que recientemente se ha recuperado. 

## <a name="constructing-a-shardmapmanager"></a>Construcción de un ShardMapManager
Un objeto **ShardMapManager** se construye mediante un patrón de [fábrica](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) . Hola  **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**  método toma las credenciales (incluido el nombre del servidor de Hola y el nombre de base de datos que contiene Hola GSM) en forma de Hola de un  **ConnectionString** y devuelve una instancia de un **ShardMapManager**.  

**Tenga en cuenta:** hello **ShardMapManager** deberían crear instancias de una sola vez por cada dominio de aplicación, en el código de inicialización de Hola para una aplicación. Creación de instancias adicionales de ShardMapManager Hola mismo appdomain, dará como resultado una mayor memoria y uso de CPU de la aplicación hello. Un objeto **ShardMapManager** puede contener cualquier número de mapas de particiones. Aunque un solo mapa de particiones puede ser suficiente para muchas aplicaciones, hay veces en que se usan diferentes conjuntos de bases de datos para un esquema diferente o con fines únicos y, en esos casos, puede que sea preferible usar varios mapas de particiones. 

En este código, una aplicación intente tooopen existente **ShardMapManager** con hello [TryGetSqlShardMapManager método](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx).  Si los objetos que representan un Global **ShardMapManager** (GSM) todavía no existe dentro de la base de datos de hello, biblioteca de cliente de hello crea existe con hello [CreateSqlShardMapManager método](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx).

    // Try tooget a reference toohello Shard Map Manager 
     // via hello Shard Map Manager database.  
    // If it doesn't already exist, then create it. 
    ShardMapManager shardMapManager; 
    bool shardMapManagerExists = ShardMapManagerFactory.TryGetSqlShardMapManager(
                                        connectionString, 
                                        ShardMapManagerLoadPolicy.Lazy, 
                                        out shardMapManager); 

    if (shardMapManagerExists) 
     { 
        Console.WriteLine("Shard Map Manager already exists");
    } 
    else
    {
        // Create hello Shard Map Manager. 
        ShardMapManagerFactory.CreateSqlShardMapManager(connectionString);
        Console.WriteLine("Created SqlShardMapManager"); 

        shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager(
            connectionString, 
            ShardMapManagerLoadPolicy.Lazy);

        // hello connectionString contains server name, database name, and admin credentials 
        // for privileges on both hello GSM and hello shards themselves.
    } 

Como alternativa, puede usar Powershell toocreate un nuevo administrador de mapa de particiones. Hay un ejemplo disponible [aquí](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).

## <a name="get-a-rangeshardmap-or-listshardmap"></a>Obtención de las clases RangeShardMap o ListShardMap
Después de crear una partición en el Administrador de mapa, puede obtener hello [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) o [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx) con hello [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), hello [ TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), o hello [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) método.

    /// <summary>
    /// Creates a new Range Shard Map with hello specified name, or gets hello Range Shard Map if it already exists.
    /// </summary>
    public static RangeShardMap<T> CreateOrGetRangeShardMap<T>(ShardMapManager shardMapManager, string shardMapName)
    {
        // Try tooget a reference toohello Shard Map.
        RangeShardMap<T> shardMap;
        bool shardMapExists = shardMapManager.TryGetRangeShardMap(shardMapName, out shardMap);

        if (shardMapExists)
        {
            ConsoleUtils.WriteInfo("Shard Map {0} already exists", shardMap.Name);
        }
        else
        {
            // hello Shard Map does not exist, so create it
            shardMap = shardMapManager.CreateRangeShardMap<T>(shardMapName);
            ConsoleUtils.WriteInfo("Created Shard Map {0}", shardMap.Name);
        }

        return shardMap;
    } 

### <a name="shard-map-administration-credentials"></a>Credenciales de administración de mapas de particiones
Las aplicaciones que administración y manipulan los mapas de particiones son diferentes de los que usan conexiones de tooroute de mapas de particiones de Hola. 

partición tooadminister se asigna (Agregar o cambiar particiones, mapas de particiones, las asignaciones de particiones, etc.) debe crear instancias de hello **ShardMapManager** con **las credenciales que tienen privilegios en ambas bases de datos GSM hello y en cada una de lectura/escritura base de datos que actúa como una partición**. las credenciales de Hello deben permitir para operaciones de escritura en tablas de hello en ambos Hola GSM y LSM como información de la asignación de particiones se especifica o se cambia, así como para crear tablas LSM en nuevas particiones.  

Vea [credenciales usan la biblioteca de cliente de base de datos elástica tooaccess hello](sql-database-elastic-scale-manage-credentials.md).

### <a name="only-metadata-affected"></a>Solo los metadatos afectados
Métodos que se utilizan para rellenar o cambiar hello **ShardMapManager** datos no alteran los datos de usuario de hello almacenados en particiones de Hola por sí mismos. Por ejemplo, los métodos como **CreateShard**, **DeleteShard**, **UpdateMapping**, etc. afectan a los metadatos de mapa de particiones de hello solo. No, quitar, agregar o modificar los datos de usuario contenidos en particiones de Hola. En su lugar, estos métodos son toobe diseñada usa junto con operaciones independientes para realiza toocreate o quitar bases de datos reales, o que mueva las filas de una partición tooanother toorebalance un entorno particionado.  (hello **dividir-combinar** herramienta que se incluye con las herramientas de base de datos elástica hace que el uso de estas API junto con la coordinación de movimiento de datos real entre las particiones.) Vea [escalado mediante la herramienta Hola bases de datos elásticas dividir-combinar](sql-database-elastic-scale-overview-split-and-merge.md).

## <a name="populating-a-shard-map-example"></a>Ejemplo de cómo rellenar un mapa de particiones
A continuación se muestra un ejemplo de secuencia de operaciones toopopulate un mapa de particiones específicos. código de Hello realiza estos pasos: 

1. Se crea un mapa de particiones en un administrador de mapas de particiones. 
2. se agregan metadatos de Hola para dos particiones diferentes toohello mapa de particiones. 
3. Se agregan una variedad de asignaciones de intervalo de claves y hello contenido global del mapa de particiones de Hola se muestra. 

Hola código está escrito para que el método hello se puede volver a ejecutar si se produce un error. Cada solicitud de prueba si una partición o la asignación ya existe antes de intentar toocreate lo. Hello código supone que las bases de datos denominan **sample_shard_0**, **sample_shard_1** y **sample_shard_2** ya se han creado en el servidor hello encontrada por cadena **shardServer**. 

    public void CreatePopulatedRangeMap(ShardMapManager smm, string mapName) 
        {            
            RangeShardMap<long> sm = null; 

            // check if shardmap exists and if not, create it 
            if (!smm.TryGetRangeShardMap(mapName, out sm)) 
            { 
                sm = smm.CreateRangeShardMap<long>(mapName); 
            } 

            Shard shard0 = null, shard1=null; 
            // Check if shard exists and if not, 
            // create it (Idempotent / tolerant of re-execute) 
            if (!sm.TryGetShard(new ShardLocation(
                                     shardServer, 
                                     "sample_shard_0"), 
                                     out shard0)) 
            { 
                Shard0 = sm.CreateShard(new ShardLocation(
                                            shardServer, 
                                            "sample_shard_0")); 
            } 

            if (!sm.TryGetShard(new ShardLocation(
                                    shardServer, 
                                    "sample_shard_1"), 
                                    out shard1)) 
            { 
                Shard1 = sm.CreateShard(new ShardLocation(
                                             shardServer, 
                                            "sample_shard_1"));  
            } 

            RangeMapping<long> rmpg=null; 

            // Check if mapping exists and if not,
            // create it (Idempotent / tolerant of re-execute) 
            if (!sm.TryGetMappingForKey(0, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                          new RangeMappingCreationInfo<long>
                          (new Range<long>(0, 50), 
                          shard0, 
                          MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(50, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(50, 100), 
                         shard1, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(100, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long>
                         (new Range<long>(100, 150), 
                         shard0, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(150, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(150, 200), 
                         shard1, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(200, out rmpg)) 
            { 
               sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(200, 300), 
                         shard0, 
                         MappingStatus.Online)); 
            } 

            // List hello shards and mappings 
            foreach (Shard s in sm.GetShards()
                         .OrderBy(s => s.Location.DataSource)
                         .ThenBy(s => s.Location.Database))
            { 
               Console.WriteLine("shard: "+ s.Location); 
            } 

            foreach (RangeMapping<long> rm in sm.GetMappings()) 
            { 
                Console.WriteLine("range: [" + rm.Value.Low.ToString() + ":" 
                        + rm.Value.High.ToString()+ ")  ==>" +rm.Shard.Location); 
            } 
        } 

Como alternativa puede usar PowerShell scripts hello tooachieve el mismo resultado. Algunos ejemplos de PowerShell de ejemplo de Hola están disponibles [aquí](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).     

Una vez que se han rellenado los mapas de particiones, aplicaciones de acceso a datos se pueden crear o adaptación toowork con mapas de Hola. Rellenar o manipular Hola mapas no necesita producirse nuevo hasta que **diseño mapa** necesita toochange.  

## <a name="data-dependent-routing"></a>Enrutamiento dependiente de los datos
Administrador de mapa de particiones de Hola se usará más en las aplicaciones que requieren operaciones de datos específicos de la aplicación de base de datos conexiones tooperform Hola. Estas conexiones deben asociarse con la base de datos correcta Hola. Esto se conoce como **Enrutamiento dependiente de los datos**. Para estas aplicaciones, instancias de un objeto de administrador de asignación de particiones de generador de hello mediante las credenciales que tienen acceso de solo lectura en la base de datos de hello GSM. Las solicitudes individuales para las conexiones posteriores proporcionan las credenciales necesarias para la conexión de base de datos de toohello particiones adecuado.

Tenga en cuenta que estas aplicaciones (mediante **ShardMapManager** abierto con las credenciales de solo lectura) no se puede realizar cambios toohello asignaciones o asignaciones. Para cubrir esas necesidades, cree aplicaciones específicas de administración o scripts de PowerShell que proporcionen credenciales con más privilegios, como se explicó anteriormente. Vea [credenciales usan la biblioteca de cliente de base de datos elástica tooaccess hello](sql-database-elastic-scale-manage-credentials.md).

Para obtener más detalles, consulte [Enrutamiento dependiente de datos](sql-database-elastic-scale-data-dependent-routing.md). 

## <a name="modifying-a-shard-map"></a>Modificación de un mapa de particiones
Un mapa de particiones puede cambiarse de distintas maneras. Todos de los siguientes métodos de Hola modifican los metadatos de Hola que describe las particiones de Hola y sus asignaciones, pero físicamente no modifican datos en particiones de hello, ni crear ni se eliminar bases de datos reales de Hola.  Algunos de las operaciones de hello en mapa de particiones de Hola que se describe a continuación pueden necesitar toobe coordinada con acciones administrativas que mover físicamente los datos o que agregar y quitar bases de datos que actúa como particiones.

Estos métodos funcionan en conjunto como bloques de creación de hello disponibles para modificar Hola distribución global de los datos en su entorno de base de datos particionada.  

* tooadd o quitar particiones: usar  **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)**  y  **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)**  de hello [Shardmap clase](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx). 
  
    Hello servidor y base de datos que representa la partición de destino de hello ya deben existir para estas operaciones tooexecute. Estos métodos no tiene ningún efecto en hello bases de datos, solo de metadatos en el mapa de particiones de Hola.
* toocreate o quitar puntos o intervalos que se asignan toohello particiones: usar  **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**,  **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)**  de hello [RangeShardMapping clase](https://msdn.microsoft.com/library/azure/dn807318.aspx), y  **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)**  de hello [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx)
  
    Muchos diferentes momentos o intervalos pueden ser asignada toohello misma partición. Estos métodos solo afectan a los metadatos, no a los datos que puedan existir ya en particiones. Si los datos tienen toobe quitado de la base de datos de hello en orden toobe coherente con **DeleteMapping** operaciones, deberá tooperform esas operaciones por separado pero junto con el uso de estos métodos.  
* toosplit rangos existente en dos o mezcla intervalos adyacentes en una sola: usar  **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)**  y  **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**.  
  
    Tenga en cuenta que divide y combinar las operaciones **no cambie la clave de toowhich de hello partición se asignan valores**. Una división divide un rango existente en dos partes, pero la deja como asignado toohello misma partición. Una combinación funciona en los dos intervalos adyacentes que ya están asignada toohello misma partición, fusión de ellas en un solo intervalo.  movimiento de puntos o intervalos de ellos mismos entre las particiones Hello necesita coordinan mediante el uso de toobe **UpdateMapping** junto con el movimiento de datos reales.  Puede usar hello **dividir y combinar** herramientas del servicio que forma parte de la base de datos elástica cambios en la asignación toocoordinate particiones con el movimiento de datos, cuando se necesita el movimiento. 
* mapa de toore (o mover) puntos o intervalos toodifferent particiones individuales: usar  **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**.  
  
    Puesto que los datos que necesite toobe movido de una partición tooanother en toobe orden coherente con **UpdateMapping** operations, necesitará tooperform este movimiento por separado pero junto con el uso de estos métodos.
* asignaciones de tootake en línea y sin conexión: usar  **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)**  y  **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)**  toocontrol Hola estado en línea de un asignación. 
  
    Solo se permite realizar determinadas operaciones en las asignaciones de particiones cuando una asignación se encuentra en un estado "sin conexión", incluidas **UpdateMapping** y **DeleteMapping**. Cuando una asignación está sin conexión, una solicitud dependiente de datos basada en una clave incluida en esa asignación devolverá un error. Además, cuando un intervalo en primer lugar se queda sin conexión, todas las particiones de toohello afectada las conexiones se eliminan automáticamente de ordenar tooprevent los resultados incoherentes o incompletos para las consultas dirigidas con intervalos que se va a cambiar. 

Las asignaciones son objetos inmutables en .NET  Todos los métodos de hello anteriores que cambiar las asignaciones de invalidarán también cualquier toothem de referencias en el código. toomake TI sea más fácil tooperform las secuencias de operaciones que cambian el estado de una asignación, todos los métodos de Hola que cambie una asignación de devuelven una nueva asignación de referencia, por lo que las operaciones se pueden encadenar. Por ejemplo, toodelete una asignación de sm shardmap que contiene la clave de hello 25 existente, puede ejecutar Hola siguientes: 

        sm.DeleteMapping(sm.MarkMappingOffline(sm.GetMappingForKey(25)));

## <a name="adding-a-shard"></a>Incorporación de una partición
Las aplicaciones a menudo necesita toosimply agregar nuevos datos de toohandle de particiones que cabe esperar de nuevas claves o intervalos de claves de un mapa de particiones que ya existe. Por ejemplo, una aplicación particionada por Id. de inquilino puede necesitar tooprovision una nueva partición para un nuevo inquilino o mensual de particiones de datos que necesite una nueva partición aprovisionada antes del inicio de Hola de nuevo cada mes. 

Si el nuevo intervalo de valores de clave de hello ya no es parte de una asignación existente y ningún movimiento de datos es necesario, es nueva partición de tooadd muy sencillo Hola y asociar la nueva clave de Hola o particiones de intervalo toothat. Para obtener más información sobre cómo agregar nuevas particiones, consulte [Incorporación de una nueva partición](sql-database-elastic-scale-add-a-shard.md).

Sin embargo, para escenarios que requieren el movimiento de datos, herramienta Dividir-combinar de hello es necesario tooorchestrate Hola el movimiento de datos entre las particiones en combinación con las actualizaciones de mapas de particiones necesarios de Hola. Para obtener más información sobre el uso de hello dividir-combinar yool, consulte [información general de la combinación de división](sql-database-elastic-scale-overview-split-and-merge.md) 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-shard-map-management/listmapping.png
[2]: ./media/sql-database-elastic-scale-shard-map-management/rangemapping.png
[3]: ./media/sql-database-elastic-scale-shard-map-management/multipleonsingledb.png
