---
title: "bibliotecas de cliente de base de datos elástica aaaUsing con Entity Framework | Documentos de Microsoft"
description: "Uso de la biblioteca de cliente de Base de datos elástica y Entity Framework para la codificación de bases de datos"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
editor: 
ms.assetid: b9c3065b-cb92-41be-aa7f-deba23e7e159
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: torsteng
ms.openlocfilehash: 917f6d28d9855c0b42afe2c008613a9bbb3ec6b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-database-client-library-with-entity-framework"></a>Biblioteca de cliente de base de datos elástica con Entity Framework
Este documento muestra los cambios de hello en una aplicación de Entity Framework que son necesario toointegrate con hello [herramientas de base de datos elástica](sql-database-elastic-scale-introduction.md). Hola es componer [administración de mapa de particiones](sql-database-elastic-scale-shard-map-management.md) y [enrutamiento dependiente de los datos](sql-database-elastic-scale-data-dependent-routing.md) con Entity Framework hello **Code First** enfoque. Hola [Code First - nueva base de datos](http://msdn.microsoft.com/data/jj193542.aspx) tutorial de EF actúa como nuestro ejemplo a lo largo de este documento. código de ejemplo de Hola que acompaña a este documento es parte de herramientas de base de datos elástica conjunto de ejemplos de hello ejemplos de código de Visual Studio.

## <a name="downloading-and-running-hello-sample-code"></a>Descargar y ejecutar código de ejemplo de Hola
código de hello toodownload de este artículo:

* Se requiere Visual Studio 2012 o posterior. 
* Descargar hello [elástico herramientas de base de datos de SQL Azure: ejemplo de integración de Entity Framework](https://code.msdn.microsoft.com/windowsapps/Elastic-Scale-with-Azure-bae904ba) de MSDN. Descomprima tooa ubicación de ejemplo de Hola de su elección.
* Inicie Visual Studio. 
* En Visual Studio, seleccione Archivo -> Abrir proyecto/solución. 
* Hola **Abrir proyecto** cuadro de diálogo, desplácese ejemplo toohello que ha descargado y seleccione **EntityFrameworkCodeFirst.sln** muestra de Hola a tooopen. 

ejemplo de Hola a toorun, necesita toocreate tres bases de datos vacías en la base de datos de SQL Azure:

* Base de datos de administrador de mapas de particiones
* Base de datos de partición 1
* Base de datos de partición 2

Una vez haya creado estas bases de datos, rellene los marcadores de posición de hello en **Program.cs** con el nombre del servidor de base de datos de SQL Azure, los nombres de base de datos de Hola y las bases de datos de credenciales tooconnect toohello. Compile la solución de hello en Visual Studio. Visual Studio descargará los paquetes de NuGet Hola necesario para la biblioteca de cliente de base de datos elástica hello, Entity Framework y control como parte del proceso de compilación de Hola de errores transitorios. Asegúrese de que la restauración de paquetes de NuGet está habilitada para la solución. Puede habilitar a esta opción con el botón secundario en el archivo de solución de Hola Hola Explorador de soluciones de Visual Studio. 

## <a name="entity-framework-workflows"></a>Flujos de trabajo de Entity Framework
Los desarrolladores de Entity Framework se basan en uno de hello siguientes cuatro aplicaciones de flujos de trabajo toobuild y persistencia de tooensure para objetos de la aplicación: 

* **Code First (base de datos nueva)**: Hola desarrollador EF crea el modelo de hello en código de la aplicación hello y, a continuación, EF genera la base de datos de Hola de él. 
* **Code First (base de datos existente)**: desarrollador Hola permite EF generar código de la aplicación hello para el modelo de Hola desde una base de datos existente.
* **Modelo primero**: desarrollador Hola crea el modelo de hello en el Diseñador de EF de hello y, a continuación, EF crea la base de datos de Hola de modelo de Hola.
* **Primero la base de datos**: programador de hello usa EF tooling modelo de hello tooinfer desde una base de datos existente. 

Todos estos métodos se basan en hello DbContext clase tootransparently administran conexiones de base de datos y el esquema de base de datos para una aplicación. Como se explica con más detalle más adelante en el documento de hello, diferentes constructores de clase base de hello DbContext permiten tener distintos niveles de control sobre la creación de la conexión, creación de arranque y el esquema de base de datos. Desafíos surgen principalmente al hecho de Hola que forma una intersección con la administración de conexión de base de datos de hello proporcionada por EF con capacidades de administración de conexión de Hola Hola datos dependientes de interfaces de enrutamiento proporciona biblioteca de cliente de base de datos elástica Hola. 

## <a name="elastic-database-tools-assumptions"></a>Suposiciones de herramientas de bases de datos elásticas
Para definiciones de términos, consulte el [Glosario de herramientas de Base de datos elástica](sql-database-elastic-scale-glossary.md).

Con la biblioteca de cliente de bases de datos elásticas, se definen particiones de los datos de la aplicación, denominadas shardlets. Se identifican mediante una clave de particionamiento y son bases de datos asignado toospecific Shardlets. Una aplicación puede tener tantas bases de datos según sea necesario y distribuir hello shardlets tooprovide suficiente capacidad o rendimiento dados los requisitos de negocios actual. asignación de Hola de bases de datos de toohello de valores de clave de particionamiento se almacena mediante un mapa de particiones proporcionado por las API de cliente de base de datos elástica Hola. A esta capacidad la denominamos **Administración de mapas de particiones**o, para abreviar, SMM. mapa de particiones de Hello también actúa como broker Hola de conexiones de base de datos para las solicitudes que llevar a cabo una clave de particionamiento. Nos referimos toothis capacidad como **enrutamiento dependiente de los datos**. 

Administrador de mapa de particiones de Hello protege a los usuarios de vistas incoherentes en datos de shardlet que se pueden producir cuando se produzcan operaciones de administración de shardlet simultáneas (por ejemplo, reubicar los datos de una partición tooanother). toodo Hola por lo tanto, administradas conexiones de base de datos de hello Service broker biblioteca de cliente hello para una aplicación de mapas de particiones. Esto permite a kill de hello particiones mapa funcionalidad tooautomatically una conexión de base de datos cuando las operaciones de administración de particiones podrían afectar a hello shardlet que se ha creado la conexión de Hola para. Este enfoque debe toointegrate con parte de la funcionalidad de EF, como la creación de nuevas conexiones desde un una toocheck existente para la existencia de base de datos. En general, la observación ha sido que constructores de DbContext estándares Hola solo la funcionan bien para las conexiones de base de datos cerrada pueden clonarse para el trabajo EF. principio de diseño de Hola de base de datos elástica en su lugar es tooonly broker abrir conexiones. Uno podría pensar que cerrar una conexión asíncrona por la biblioteca de cliente de hello antes de entregarlo a través de toohello EF DbContext podría solucionar este problema. Sin embargo, al cerrar la conexión de Hola y confiar en EF toore al abrir, uno foregoes comprobaciones de validación y la coherencia de Hola Hola biblioteca realizadas. la funcionalidad de migraciones de Hello en EF, sin embargo, usa estos Hola de toomanage conexiones esquema de base de datos de forma que sea transparente toohello aplicación subyacente. Idealmente, se desea tooretain y combinar todas estas capacidades de la biblioteca de cliente de base de datos elástica hello y EF Hola misma aplicación. Hello siguiente sección describen estas propiedades y los requisitos con más detalle. 

## <a name="requirements"></a>Requisitos
Cuando se trabaja con la biblioteca de cliente de base de datos elástica hello y las API de Entity Framework, queremos hello tooretain propiedades siguientes: 

* **Escalado horizontal**: tooadd o quitar bases de datos de capa de datos de Hola de aplicación particionada hello según sea necesario para las demandas de capacidad de Hola de aplicación hello. Esto significa que un control sobre la creación de Hola Hola y eliminación de bases de datos y utilizando Hola bases de datos elásticas particiones manager API toomanage las bases de datos y las asignaciones de shardlets. 
* **Coherencia**: aplicación hello emplea particionamiento y utiliza Hola capacidades de enrutamiento dependiente de datos de biblioteca de cliente de Hola. tooavoid daños o resultados de la consulta incorrecta, las conexiones se pasa por el Administrador de mapa de particiones de Hola. También mantiene la validación y la coherencia.
* **Code First**: comodidad de hello tooretain del primer paradigma del EF código. En Code First, las clases de aplicación Hola se asignan de forma transparente toohello subyacente estructuras de base de datos. código de la aplicación Hello interactúa con DbSets que enmascarar la mayoría de los aspectos implicados en hello subyacente de procesamiento de la base de datos.
* **Esquema**: Entity Framework controla la creación del esquema de base de datos inicial y la evolución del esquema posterior a través de migraciones. Al conservar estas capacidades, es fácil como Hola datos evoluciona adaptar la aplicación. 

Hello siguiente orientación indica a cómo toosatisfy estos requisitos para las aplicaciones de Code First con herramientas de base de datos elástica. 

## <a name="data-dependent-routing-using-ef-dbcontext"></a>Enrutamiento dependiente de datos con DbContext de EF
Las conexiones de base de datos con Entity Framework se suelen administrar mediante subclases de **DbContext**. Cree estas subclases basándose en **DbContext**. Aquí es donde se define la **DbSets** que implementar colecciones de seguridad de base de datos de Hola de objetos CLR para la aplicación. En el contexto de Hola de enrutamiento dependiente de datos, podemos identificar varias propiedades útiles que no tienen necesariamente para otros escenarios de aplicación EF primer de código: 

* base de datos de Hello ya existe y se ha registrado en el mapa de particiones de bases de datos elásticas Hola. 
* esquema de Hola de aplicación hello ya ha sido implementado toohello base de datos (se explica más adelante). 
* Base de datos de dependiente de los datos enrutamiento conexiones toohello se asíncrona al mapa de particiones de Hola. 

toointegrate **DbContexts** con enrutamiento dependiente de los datos para la implementación escalada:

1. Crear conexiones de base de datos física a través de interfaces de cliente de base de datos elástica Hola de administrador de asignación de particiones de hello, 
2. Ajustar la conexión de hello con hello **DbContext** subclase
3. Pasar de conexión de hello hacia abajo en hello **DbContext** base tooensure clases todo el procesamiento de hello en lado EF Hola sucede así. 

Hola, ejemplo de código siguiente muestra este enfoque. (Este código también es Hola que acompaña a proyecto de Visual Studio)

    public class ElasticScaleContext<T> : DbContext
    {
    public DbSet<Blog> Blogs { get; set; }
    …

        // C'tor for data dependent routing. This call will open a validated connection 
        // routed toohello proper shard by hello shard map manager. 
        // Note that hello base class c'tor call will fail for an open connection
        // if migrations need toobe done and SQL credentials are used. This is hello reason for hello 
        // separation of c'tors into hello data-dependent routing case (this c'tor) and hello internal c'tor for new shards.
        public ElasticScaleContext(ShardMap shardMap, T shardingKey, string connectionStr)
            : base(CreateDDRConnection(shardMap, shardingKey, connectionStr), 
            true /* contextOwnsConnection */)
        {
        }

        // Only static methods are allowed in calls into base class c'tors.
        private static DbConnection CreateDDRConnection(
        ShardMap shardMap, 
        T shardingKey, 
        string connectionStr)
        {
            // No initialization
            Database.SetInitializer<ElasticScaleContext<T>>(null);

            // Ask shard map toobroker a validated connection for hello given key
            SqlConnection conn = shardMap.OpenConnectionForKey<T>
                                (shardingKey, connectionStr, ConnectionOptions.Validate);
            return conn;
        }    

## <a name="main-points"></a>Puntos principales
* Un nuevo constructor reemplaza el constructor predeterminado de hello en subclase de DbContext Hola 
* Hola nuevo constructor usa argumentos de Hola que son necesarios para el enrutamiento dependiente de datos a través de la biblioteca de cliente de base de datos elástica:
  
  * tooaccess de mapa de particiones de Hola Hola interfaces de enrutamiento dependiente de los datos,
  * Hola particionamiento tooidentify clave hello shardlet,
  * una cadena de conexión con credenciales de hello para la partición del toohello de conexión de enrutamiento Hola dependiente de los datos. 
* constructor de clase base en toohello Hola llamada toma un desvío en un método estático que lleva a cabo todos los pasos de hello necesaria para el enrutamiento dependiente de los datos. 
  
  * Utiliza llamadas de OpenConnectionForKey Hola de interfaces de cliente de base de datos elástica hello en hello particiones mapa tooestablish una conexión abierta.
  * mapa de particiones de Hello crea particiones de toohello de conexión abierta de Hola que contiene shardlet Hola Hola clave de particionamiento dada.
  * Esta conexión abierta se pasa el constructor de clase base toohello atrás de tooindicate DbContext que esta conexión es toobe usa EF en lugar de dejar que EF cree automáticamente una nueva conexión. Esta conexión de manera Hola se ha etiquetado por la API de cliente de base de datos elástica Hola para que se pueda garantizar la coherencia en las operaciones de administración de mapa de particiones.

Use Hola nuevo constructor de la subclase DbContext en lugar del constructor predeterminado de hello en el código. Aquí tiene un ejemplo: 

    // Create and save a new blog.

    Console.Write("Enter a name for a new blog: "); 
    var name = Console.ReadLine(); 

    using (var db = new ElasticScaleContext<int>( 
                            sharding.ShardMap,  
                            tenantId1,  
                            connStrBldr.ConnectionString)) 
    { 
        var blog = new Blog { Name = name }; 
        db.Blogs.Add(blog); 
        db.SaveChanges(); 

        // Display all Blogs for tenant 1 
        var query = from b in db.Blogs 
                    orderby b.Name 
                    select b; 
     … 
    }

Abre el nuevo constructor de Hello particiones toohello de hello conexión que contiene datos de Hola para shardlet Hola identificado por el valor de Hola de **tenantid1**. Hola código de hello **con** bloque permanece sin cambios tooaccess hello **DbSet** para los blogs con EF en particiones de Hola para **tenantid1**. Esto cambia la semántica de código de hello en hello mediante el bloque de modo que todas las operaciones de base de datos ahora ámbito toohello una partición donde **tenantid1** se mantiene. Por ejemplo, una consulta LINQ a través de blogs de hello **DbSet** podría devolver solo los blogs almacenados en la partición actual de hello, pero no Hola a los que se almacenan en otras particiones.  

#### <a name="transient-faults-handling"></a>Control de errores transitorios
Hello Microsoft Patterns & Practices equipo Hola publicado [Hola Transient Fault Handling Application Block](https://msdn.microsoft.com/library/dn440719.aspx). biblioteca de Hola se usa con la biblioteca de cliente de escala elástica en combinación con EF. Sin embargo, asegúrese de que cualquier excepción transitoria devuelve lugar tooa donde es posible garantizar que ese nuevo constructor Hola está usándola después de un error transitorio para que cualquier nuevo intento de conexión se realiza mediante constructores Hola que nos hemos ajustado. En caso contrario, se mantiene un toohello de conexión correcto no se garantiza la partición y no hay ninguna garantía de conexión hello como cambios que se producen toohello mapa de particiones. 

Hello ejemplo de código siguiente muestra cómo una directiva de reintentos SQL puede utilizarse alrededor de hello nueva **DbContext** constructores de subclase: 

    SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() => 
    { 
        using (var db = new ElasticScaleContext<int>( 
                                sharding.ShardMap,  
                                tenantId1,  
                                connStrBldr.ConnectionString)) 
            { 
                    var blog = new Blog { Name = name }; 
                    db.Blogs.Add(blog); 
                    db.SaveChanges(); 
            … 
            } 
        }); 

**SqlDatabaseUtils.SqlRetryPolicy** en hello código anterior se define como un **SqlDatabaseTransientErrorDetectionStrategy** con un número de reintentos de 10 y 5 segundos de tiempo entre los reintentos de espera. Este enfoque es similar Guía de toohello para EF y las transacciones iniciadas por el usuario (consulte [limitaciones con reintentando estrategias de ejecución (en adelante EF6)](http://msdn.microsoft.com/data/dn307226). Ambas situaciones requieren ese programa de aplicación Hola controla Hola ámbito toowhich Hola excepción transitoria devuelve: tooeither vuelva a abrir la transacción de Hola o (tal y como se muestra), volver a crear contexto de Hola de constructor adecuado de Hola que usa Hola bases de datos elásticas biblioteca de cliente.

Hello toocontrol necesario en las excepciones transitorias nos adoptar en el ámbito también evita que las use Hola integrados de Hola de **SqlAzureExecutionStrategy** que viene con EF. **SqlAzureExecutionStrategy** debería volver a abrir una conexión pero no usar **OpenConnectionForKey** y, por tanto, omitir todas las validaciones de Hola que se realizan como parte del programa Hola a **OpenConnectionForKey** llamar. En su lugar, ejemplo de código de hello usa integradas de hello **DefaultExecutionStrategy** que también se proporciona con EF. En lugar de demasiado**SqlAzureExecutionStrategy**, funciona correctamente en combinación con la directiva de reintento de hello del control de errores transitorios. Directiva de ejecución de Hola se establece en hello **ElasticScaleDbConfiguration** clase. Tenga en cuenta que decidimos no toouse **DefaultSqlExecutionStrategy** desde que sugiere toouse **SqlAzureExecutionStrategy** si se producen las excepciones transitorias - que provocaban toowrong comportamiento tal como se describe. Para obtener más información sobre las directivas de reintento diferentes de Hola y EF, consulte [resistencia de conexión en EF](http://msdn.microsoft.com/data/dn456835.aspx).     

#### <a name="constructor-rewrites"></a>Reescrituras del constructor
ejemplos de código anteriores Hello ilustran predeterminado de hello constructor reescribe necesario para la aplicación en orden toouse depende de los datos de enrutamiento con hello Entity Framework. Hello en la tabla siguiente generaliza esta constructores tooother de enfoque. 

| Constructor actual | Constructor reescrito para datos | Constructor base | Notas |
| --- | --- | --- | --- |
| MyContext() |ElasticScaleContext(ShardMap, TKey) |DbContext(DbConnection, bool) |conexión de Hello debe toobe una función de mapa de particiones de Hola y clave de enrutamiento Hola dependiente de los datos. Creación de la conexión automática de tooby pasada por parte de EF es necesario y en su lugar use conexión de hello particiones mapa toobroker Hola. |
| MyContext(string) |ElasticScaleContext(ShardMap, TKey) |DbContext(DbConnection, bool) |conexión de Hello es una función de mapa de particiones de Hola y la clave de enrutamiento de hello dependiente de los datos. Una cadena de nombre o una conexión de base de datos fija no funcionará como validación eludir mediante el mapa de particiones de Hola. |
| MyContext(DbCompiledModel) |ElasticScaleContext(ShardMap, TKey, DbCompiledModel) |DbContext(DbConnection, DbCompiledModel, bool) |conexión de Hello obtener creará para hello tiene clave de particionamiento y de mapa de particiones con el modelo de hello proporcionado. Hola compilado modelo se pasarán en toohello base c'tor. |
| MyContext(DbConnection, bool) |ElasticScaleContext(ShardMap, TKey, bool) |DbContext(DbConnection, bool) |conexión de Hello debe toobe inferir de mapa de particiones de Hola y la clave de Hola. No se pueden proporcionar como entrada (a menos que ya estaba usando esa entrada mapa de particiones de Hola y la clave de hello). Hola booleano se pasarán en. |
| MyContext(string, DbCompiledModel) |ElasticScaleContext(ShardMap, TKey, DbCompiledModel) |DbContext(DbConnection, DbCompiledModel, bool) |conexión de Hello debe toobe inferir de mapa de particiones de Hola y la clave de Hola. No se pueden proporcionar como entrada (a menos que estaba usando esa entrada mapa de particiones de Hola y la clave de hello). Hola compilado modelo se pasarán en. |
| MyContext(ObjectContext, bool) |ElasticScaleContext(ShardMap, TKey, ObjectContext, bool) |DbContext(ObjectContext, bool) |constructor new Hello debe tooensure que las conexiones de hello que ObjectContext se pasa como entrada es conexión vuelve a enrutarse tooa administrado por la escala elástica. Es una explicación detallada de ObjectContexts más allá del ámbito de Hola de este documento. |
| MyContext(DbConnection, DbCompiledModel,bool) |ElasticScaleContext(ShardMap, TKey, DbCompiledModel, bool) |DbContext(DbConnection, DbCompiledModel, bool); |conexión de Hello debe toobe inferir de mapa de particiones de Hola y la clave de Hola. conexión de Hello no se pueden proporcionar como entrada (a menos que ya estaba usando esa entrada mapa de particiones de Hola y la clave de hello). Modelo y un valor booleano se pasan en el constructor de clase base toohello. |

## <a name="shard-schema-deployment-through-ef-migrations"></a>Implementación del esquema de partición mediante migraciones de EF
Administración automática de esquemas es una comodidad que ofrece Hola Entity Framework. En el contexto de Hola de aplicaciones mediante herramientas de base de datos elástica, queremos tooretain este particiones capacidad tooautomatically aprovisionar Hola esquema toonewly creado cuando las bases de datos se agregan aplicación particionada toohello. Hola uso principal es la capacidad de tooincrease en la capa de datos de Hola para aplicaciones con particiones mediante EF. Confiar en las capacidades de EF para administrar el esquema reduce el esfuerzo de administración de base de datos de hello con una aplicación particionada basada en EF. 

La implementación del esquema a través de migraciones de EF funciona mejor en **conexiones sin abrir**. En cambio trata toohello escenario de enrutamiento dependiente de datos que se basa en conexión Hola abierto proporcionado por la API de cliente de base de datos elástica Hola. Otra diferencia es el requisito de coherencia de hello: al tooensure deseable coherencia para todos los datos dependientes enrutamiento conexiones tooprotect contra la manipulación de mapa de particiones simultáneas, no es un problema con la base de datos de esquema inicial implementación tooa nueva que tiene todavía no se ha registrado en el mapa de particiones de Hola y todavía no ha asignado toohold shardlets. Por lo tanto, podemos dependen conexiones de base de datos normal para esta escenarios, como el enrutamiento de toodata dependiente opuestos.  

Esto conduce a tooan enfoque donde implementación del esquema a través de las migraciones de EF está asociado estrechamente al registro de hello de base de datos nueva hello como una partición en el mapa de particiones de la aplicación hello. Esto se basa en hello siguiendo los requisitos previos: 

* base de datos de Hello ya se ha creado. 
* base de datos de Hello está vacío, contiene ningún esquema de usuario y no hay datos de usuario.
* base de datos de Hello aún no son accesibles a través de las API de cliente de base de datos elástica hello para el enrutamiento dependiente de los datos. 

Con estos requisitos previos en su lugar, podemos crear normal sin abierto **SqlConnection** tookick desactivar las migraciones de EF para la implementación del esquema. Hola siguiendo el ejemplo de código muestra este enfoque. 

        // Enter a new shard - i.e. an empty database - toohello shard map, allocate a first tenant tooit  
        // and kick off EF intialization of hello database toodeploy schema 

        public void RegisterNewShard(string server, string database, string connStr, int key) 
        { 

            Shard shard = this.ShardMap.CreateShard(new ShardLocation(server, database)); 

            SqlConnectionStringBuilder connStrBldr = new SqlConnectionStringBuilder(connStr); 
            connStrBldr.DataSource = server; 
            connStrBldr.InitialCatalog = database; 

            // Go into a DbContext tootrigger migrations and schema deployment for hello new shard. 
            // This requires an un-opened connection. 
            using (var db = new ElasticScaleContext<int>(connStrBldr.ConnectionString)) 
            { 
                // Run a query tooengage EF migrations 
                (from b in db.Blogs 
                    select b).Count(); 
            } 

            // Register hello mapping of hello tenant toohello shard in hello shard map. 
            // After this step, data-dependent routing on hello shard map can be used 

            this.ShardMap.CreatePointMapping(key, shard); 
        } 


Este ejemplo muestra el método hello **RegisterNewShard** que registros Hola particiones en mapa de particiones de hello, implementa el esquema de Hola a través de las migraciones de EF y almacena una asignación de una partición de toohello clave de particionamiento. Se basa en un constructor de hello **DbContext** subclase (**ElasticScaleContext** en el ejemplo de Hola) que toma una cadena de conexión de SQL como entrada. código de Hello de este constructor es sencilla, como Hola siguiente ejemplo se muestra: 

        // C'tor toodeploy schema and migrations tooa new shard 
        protected internal ElasticScaleContext(string connectionString) 
            : base(SetInitializerForConnection(connectionString)) 
        { 
        } 

        // Only static methods are allowed in calls into base class c'tors 
        private static string SetInitializerForConnection(string connnectionString) 
        { 
            // We want existence checks so that hello schema can get deployed 
            Database.SetInitializer<ElasticScaleContext<T>>( 
        new CreateDatabaseIfNotExists<ElasticScaleContext<T>>()); 

            return connnectionString; 
        } 

Una posible que haya usado la versión Hola de constructor Hola que se hereda de la clase base Hola. Pero Hola código necesidades tooensure que Hola inicializador de manera predeterminada para EF se utiliza al conectarse. Por lo tanto, Hola desvío corto en el método estático de hello antes de llamar al constructor de clase base Hola con cadena de conexión de Hola. Tenga en cuenta que el registro de hello de particiones debe ejecutarse en un tooensure de dominio o un proceso de aplicación distinta configuración de inicializador de Hola para EF no entren en conflicto. 

## <a name="limitations"></a>Limitaciones
enfoques de Hola que se describen en este documento implican un par de limitaciones: 

* Las aplicaciones de EF que utilizan **LocalDb** necesita primero la base de datos de SQL Server normal de toomigrate tooa antes de usar la biblioteca de cliente de base de datos elástica. El escalado horizontal de una aplicación mediante particionamiento con Escalado elástico no es posible con **LocalDb**. Tenga en cuenta que los desarrolladores pueden seguir usando **LocalDb**. 
* Cualquier aplicación de toohello de cambios que implican cambios de esquema de base de datos necesita toogo a través de las migraciones de EF en todas las particiones. código de ejemplo de Hola para este documento no se muestra cómo toodo esto. Considere el uso de Update-Database con una tooiterate de parámetro ConnectionString sobre todas las particiones; ni un script de Hola T-SQL de extracción para hello pendiente de migración mediante Update-Database con Hola - opción de secuencia de comandos y aplicar particiones de tooyour de script de Hola T-SQL.  
* Dada una solicitud, se asume que todo el procesamiento de la base de datos está contenido en una sola partición identificada por la clave de particionamiento de hello proporcionada por solicitud de saludo. Sin embargo, esta suposición no siempre es cierta. Por ejemplo, cuando no es posible toomake una clave de particionamiento disponible. tooaddress, Hola biblioteca de cliente proporciona hello **MultiShardQuery** clase que implementa una abstracción de conexión para las consultas en varias particiones. Aprendizaje hello toouse **MultiShardQuery** en combinación con EF está más allá del ámbito de Hola de este documento

## <a name="conclusion"></a>Conclusión
Hola pasos que se describen en este documento, aplicaciones de EF pueden utilizar capacidad de la biblioteca de cliente de hello elástico de base de datos para datos que dependen de enrutamiento mediante la refactorización de constructores de hello **DbContext** subclases usa Hola EF aplicación. Este límites Hola requerían toothose los lugares donde **DbContext** clases ya existen. Además, las aplicaciones de EF pueden seguir toobenefit de implementación automática de esquemas mediante la combinación de pasos de Hola que invocan Hola necesarios EF migraciones con el registro de hello de nuevas particiones y las asignaciones en el mapa de particiones de Hola. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-use-entity-framework-applications-visual-studio/sample.png
