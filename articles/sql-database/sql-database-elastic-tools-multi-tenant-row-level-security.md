---
title: "aplicaciones de inquilinos de aaaMulti con las herramientas de bases de datos elásticas y seguridad de nivel de fila"
description: "Obtenga información acerca de cómo toouse herramientas de base de datos elástica junto con nivel de fila seguridad toobuild una aplicación con un nivel de datos altamente escalable en la base de datos de SQL de Azure que admite varios inquilinos particiones."
metakeywords: azure sql database elastic tools multi tenant row level security rls
services: sql-database
documentationcenter: 
manager: jhubbard
author: tmullaney
ms.assetid: e72d3cfe-e9be-4326-b776-9c6d96c0a18e
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: thmullan;torsteng
ms.openlocfilehash: e00076a8db4a295374993aedd49f2318bd4d701d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="multi-tenant-applications-with-elastic-database-tools-and-row-level-security"></a>Aplicaciones de múltiples inquilinos con herramientas de bases de datos elásticas y seguridad de nivel de fila
[Herramientas de base de datos elástica](sql-database-elastic-scale-get-started.md) y [(RLS) de seguridad de nivel de fila](https://msdn.microsoft.com/library/dn765131) ofrecen un conjunto eficaz de capacidades de manera flexible y eficaz escalar la capa de datos de Hola de una aplicación multiempresa con base de datos de SQL Azure. Consulte [Modelos de diseño para las aplicaciones SaaS multiinquilino con base de datos SQL de Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md) para obtener más información. 

Este artículo se explica cómo toouse estos toobuild de tecnologías conjuntamente una aplicación con un nivel de datos altamente escalable que es compatible con particiones de varios inquilinos, con **ADO.NET SqlClient** o **deEntityFramework**.  

* **Herramientas de base de datos elástica** permite a los desarrolladores tooscale fuera de la capa de datos de Hola de una aplicación a través de procedimientos recomendados de particionamiento estándar del sector mediante un conjunto de plantillas de servicio de Azure y bibliotecas de. NET. Administración de particiones con el uso de hello elástico biblioteca de cliente de base de datos le ayuda a automatizar y simplificar muchas de tareas los Hola normalmente asociadas con el particionamiento. 
* **Seguridad de nivel de fila** permite que los desarrolladores toostore datos para varios inquilinos en la misma base de datos utilizando toofilter de directivas de seguridad las filas que no pertenecen a los inquilinos toohello ejecutar una consulta de Hola. Centralizar la lógica de acceso con RLS dentro de la base de datos de hello, en su lugar de en la aplicación hello, simplifica el mantenimiento y reduce el riesgo de Hola de error como una aplicación codebase aumenta de tamaño. 

Uso de estas características juntas, una aplicación puede beneficiarse de las mejoras de ahorro y eficiencia de costo mediante el almacenamiento de datos para varios inquilinos en hello mismo base de datos de partición. Hola mismo tiempo, una aplicación todavía tiene Hola flexibilidad toooffer aislada, único inquilino particiones para los inquilinos de "premium" que se requieren garantías de rendimiento más estrictas, puesto que las particiones de varios inquilinos no garantizan la distribución de recursos igual entre los inquilinos.  

En resumen, Hola de la biblioteca de cliente de base de datos elástica [enrutamiento dependiente de datos](sql-database-elastic-scale-data-dependent-routing.md) API conectan automáticamente los inquilinos toohello partición correcta base de datos con su clave de particionamiento (generalmente un "TenantId"). Una vez conectado, una directiva de seguridad RLS dentro de la base de datos de hello garantiza que los inquilinos sólo pueden tener acceso a las filas que contienen su TenantId. Se supone que todas las tablas contienen un tooindicate de columna de TenantId qué filas pertenecen a tooeach inquilino. 

![Arquitectura de la aplicación de creación de blogs][1]

## <a name="download-hello-sample-project"></a>Descargar el proyecto de ejemplo de Hola
### <a name="prerequisites"></a>Requisitos previos
* Uso de Visual Studio (2012 o posterior) 
* Creación de tres Bases de datos SQL de Azure 
* Descargue el proyecto de ejemplo: [Herramientas de bases de datos elásticas para SQL de Azure - Particiones con varios inquilinos](http://go.microsoft.com/?linkid=9888163)
  * Rellenar la información de Hola para las bases de datos al principio de Hola de **Program.cs** 

Este proyecto extiende Hola uno se describe en [elástico herramientas de base de datos de SQL Azure - integración de Entity Framework](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md) agregando compatibilidad para las bases de datos de la partición de varios inquilinos. Se crea una aplicación de consola sencilla para la creación de blogs y publicaciones, con cuatro de los inquilinos y dos bases de datos de partición de varios inquilinos como se muestra en hello diagrama anterior. 

Compile y ejecute la aplicación hello. Esto arranca herramientas Hola elástico de base de datos Administrador de mapa de particiones y ejecución Hola después de pruebas: 

1. Con Entity Framework y LINQ, cree un nuevo blog y muestre todos los blogs para cada inquilino.
2. Con ADO.NET SqlClient, muestre todos los blogs para un inquilino.
3. Intente tooinsert blog para hello inquilino incorrecto tooverify que se produce un error  

Observe que, porque todavía no se ha habilitado RLS en bases de datos de partición de Hola, cada una de estas pruebas revela un problema: los inquilinos están toosee capaz de blogs que no pertenecen toothem y aplicación hello no se les impide insertar un blog del inquilino incorrecto de Hola. Hello que queda de este artículo describe cómo tooresolve estos problemas mediante la aplicación de inquilino aislamiento con RLS. Hay dos pasos: 

1. **Capa de aplicación**: modificar el código de la aplicación hello tooalways conjunto Hola TenantId actual en hello SESSION_CONTEXT después de abrir una conexión. proyecto de ejemplo de Hola ya ha hecho. 
2. **Capa de datos**: crear una directiva de seguridad RLS en cada toofilter de base de datos de partición filas basadas en hello TenantId almacenados en SESSION_CONTEXT. Deberá toodo esto para cada una de las bases de datos de la partición; en caso contrario, no se filtrarán filas en particiones de varios inquilinos. 

## <a name="step-1-application-tier-set-tenantid-in-hello-sessioncontext"></a>Capa de aplicación del paso 1): establezca TenantId en hello SESSION_CONTEXT
Después de conectar tooa particiones base de datos con datos de la biblioteca de cliente de base de datos elástica Hola que todavía la API de enrutamientos dependientes, aplicación hello necesidades de base de datos de tootell Hola qué TenantId usa esa conexión para que una directiva de seguridad RLS puede filtrar las filas tooother, que pertenecen los inquilinos. Hola toopass manera recomendada esta información es toostore Hola TenantId actual para esa conexión en hello [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806.aspx). (Nota: como alternativa, podría usar [CONTEXT_INFO](https://msdn.microsoft.com/library/ms180125.aspx), pero SESSION_CONTEXT constituye una mejor opción porque es más fácil toouse, devuelve NULL de forma predeterminada y admite pares de clave y valor.)

### <a name="entity-framework"></a>Entity Framework
Para las aplicaciones que usan Entity Framework, un enfoque más sencillo Hola es hello tooset SESSION_CONTEXT dentro de hello ElasticScaleContext invalidar se describe en [enrutamiento dependiente de datos mediante EF DbContext](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md#data-dependent-routing-using-ef-dbcontext). Antes de devolver la conexión de hello asíncrona a través de enrutamiento dependiente de datos, crear y ejecutar un objeto SqlCommand que establece 'TenantId' en hello SESSION_CONTEXT toohello shardingKey especificada para esa conexión. De este modo, solo necesita toowrite código una vez tooset Hola SESSION_CONTEXT. 

```
// ElasticScaleContext.cs 
// ... 
// C'tor for data dependent routing. This call will open a validated connection routed toohello proper 
// shard by hello shard map manager. Note that hello base class c'tor call will fail for an open connection 
// if migrations need toobe done and SQL credentials are used. This is hello reason for hello  
// separation of c'tors into hello DDR case (this c'tor) and hello internal c'tor for new shards. 
public ElasticScaleContext(ShardMap shardMap, T shardingKey, string connectionStr)
    : base(OpenDDRConnection(shardMap, shardingKey, connectionStr), true /* contextOwnsConnection */)
{
}

public static SqlConnection OpenDDRConnection(ShardMap shardMap, T shardingKey, string connectionStr)
{
    // No initialization
    Database.SetInitializer<ElasticScaleContext<T>>(null);

    // Ask shard map toobroker a validated connection for hello given key
    SqlConnection conn = null;
    try
    {
        conn = shardMap.OpenConnectionForKey(shardingKey, connectionStr, ConnectionOptions.Validate);

        // Set TenantId in SESSION_CONTEXT tooshardingKey tooenable Row-Level Security filtering
        SqlCommand cmd = conn.CreateCommand();
        cmd.CommandText = @"exec sp_set_session_context @key=N'TenantId', @value=@shardingKey";
        cmd.Parameters.AddWithValue("@shardingKey", shardingKey);
        cmd.ExecuteNonQuery();

        return conn;
    }
    catch (Exception)
    {
        if (conn != null)
        {
            conn.Dispose();
        }

        throw;
    }
} 
// ... 
```

Ahora hello SESSION_CONTEXT se establece automáticamente con hello especifica TenantId siempre que se invoca ElasticScaleContext: 

```
// Program.cs 
SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() => 
{   
    using (var db = new ElasticScaleContext<int>(sharding.ShardMap, tenantId, connStrBldr.ConnectionString))   
    {     
        var query = from b in db.Blogs
                    orderby b.Name
                    select b;

        Console.WriteLine("All blogs for TenantId {0}:", tenantId);     
        foreach (var item in query)     
        {       
            Console.WriteLine(item.Name);     
        }   
    } 
}); 
```

### <a name="adonet-sqlclient"></a>SqlClient de ADO.NET
Para aplicaciones que utilizan ADO.NET SqlClient, hello recomienda consiste toocreate una función de contenedor alrededor de ShardMap.OpenConnectionForKey() que establece automáticamente 'TenantId' en hello SESSION_CONTEXT toohello corregir TenantId antes de devolver un conexión. tooensure que SESSION_CONTEXT siempre se establece, solo se deben abrir las conexiones que utilizan esta función de contenedor.

```
// Program.cs
// ...

// Wrapper function for ShardMap.OpenConnectionForKey() that automatically sets SESSION_CONTEXT with hello correct
// tenantId before returning a connection. As a best practice, you should only open connections using this 
// method tooensure that SESSION_CONTEXT is always set before executing a query.
public static SqlConnection OpenConnectionForTenant(ShardMap shardMap, int tenantId, string connectionStr)
{
    SqlConnection conn = null;
    try
    {
        // Ask shard map toobroker a validated connection for hello given key
        conn = shardMap.OpenConnectionForKey(tenantId, connectionStr, ConnectionOptions.Validate);

        // Set TenantId in SESSION_CONTEXT tooshardingKey tooenable Row-Level Security filtering
        SqlCommand cmd = conn.CreateCommand();
        cmd.CommandText = @"exec sp_set_session_context @key=N'TenantId', @value=@shardingKey";
        cmd.Parameters.AddWithValue("@shardingKey", tenantId);
        cmd.ExecuteNonQuery();

        return conn;
    }
    catch (Exception)
    {
        if (conn != null)
        {
            conn.Dispose();
        }

        throw;
    }
}

// ...

// Example query via ADO.NET SqlClient
// If row-level security is enabled, only Tenant 4's blogs will be listed
SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() =>
{
    using (SqlConnection conn = OpenConnectionForTenant(sharding.ShardMap, tenantId4, connStrBldr.ConnectionString))
    {
        SqlCommand cmd = conn.CreateCommand();
        cmd.CommandText = @"SELECT * FROM Blogs";

        Console.WriteLine("--\nAll blogs for TenantId {0} (using ADO.NET SqlClient):", tenantId4);
        SqlDataReader reader = cmd.ExecuteReader();
        while (reader.Read())
        {
            Console.WriteLine("{0}", reader["Name"]);
        }
    }
});

```

## <a name="step-2-data-tier-create-row-level-security-policy"></a>Paso 2) Capa de datos: cree una directiva de seguridad de nivel de fila
### <a name="create-a-security-policy-toofilter-hello-rows-each-tenant-can-access"></a>Crear un hello toofilter de directiva de seguridad filas que pueden tener acceso todos los inquilinos
Ahora que la aplicación hello es establecer SESSION_CONTEXT con Hola TenantId actual antes de consultar, una directiva de seguridad RLS puede filtrar las consultas y excluir filas que tienen un valor de TenantId diferentes.  

RLS se implementa en código T-SQL: una función definida por el usuario define la lógica de acceso de hello y una directiva de seguridad enlaza este número de tooany de función de tablas. Para este proyecto, función hello simplemente comprobará que Hola aplicación (en lugar de algún otro usuario SQL) es la base de datos de toohello conectado, y ese hello 'TenantId' almacenado en hello SESSION_CONTEXT coincide con hello TenantId de una fila determinada. Un predicado de filtro le permitirá las filas que cumplen estas condiciones toopass a través del filtro de Hola para consultas SELECT, UPDATE y DELETE; y un predicado block que impedirá que las filas que infringen estas condiciones que insertados o actualizados. Si no se ha establecido SESSION_CONTEXT, devolverá que null y no hay ninguna fila será toobe visible o puede insertar. 

tooenable RLS, ejecute hello siguiente T-SQL en todas las particiones con cualquier Visual Studio (SSDT), SSMS, u Hola script de PowerShell incluido en el proyecto de hello (o si está utilizando [elástico de base de datos de trabajos](sql-database-elastic-jobs-overview.md), se puede usar tooautomate ejecución de esta instrucción T-SQL en todas las particiones): 

```
CREATE SCHEMA rls -- separate schema tooorganize RLS objects 
GO

CREATE FUNCTION rls.fn_tenantAccessPredicate(@TenantId int)     
    RETURNS TABLE     
    WITH SCHEMABINDING
AS
    RETURN SELECT 1 AS fn_accessResult          
        WHERE DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('dbo') -- hello user in your application’s connection string (dbo is only for demo purposes!)         
        AND CAST(SESSION_CONTEXT(N'TenantId') AS int) = @TenantId
GO

CREATE SECURITY POLICY rls.tenantAccessPolicy
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Blogs,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Blogs,
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Posts,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Posts
GO 
```

> [!TIP]
> Para los proyectos más complejos que necesitan tooadd predicado de hello en cientos de tablas, puede utilizar un procedimiento almacenado auxiliar que genera automáticamente una directiva de seguridad que se agrega un predicado en todas las tablas en un esquema. Vea [tablas de aplicar la seguridad de nivel de fila tooall - script auxiliar (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/03/31/apply-row-level-security-to-all-tables-helper-script).  
> 
> 

Ahora si se ejecuta de nuevo la aplicación de ejemplo de Hola, los inquilinos le pueda toosee solo las filas que pertenecen a toothem. Además, aplicación hello no pueden insertar filas que pertenecen tootenants que no sea de base de datos de hello toohello conectado actualmente una partición, y no puede actualizar filas visibles toohave un valor de TenantId diferentes. Si hay aplicación hello intentos toodo o bien, se generará una DbUpdateException.

Si agrega una nueva tabla más adelante, simplemente ALTER Hola directiva de seguridad y agregue los predicados de filtro y de bloqueo en la nueva tabla de Hola: 

```
ALTER SECURITY POLICY rls.tenantAccessPolicy     
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable
GO 
```

### <a name="add-default-constraints-tooautomatically-populate-tenantid-for-inserts"></a>Agregar de forma predeterminada restricciones tooautomatically rellenar TenantId para las inserciones
Puede colocar un valor predeterminado restricción en cada tabla tooautomatically rellenar hello TenantId con hello valor almacenado actualmente en SESSION_CONTEXT al insertar filas. Por ejemplo: 

```
-- Create default constraints tooauto-populate TenantId with hello value of SESSION_CONTEXT for inserts 
ALTER TABLE Blogs     
    ADD CONSTRAINT df_TenantId_Blogs      
    DEFAULT CAST(SESSION_CONTEXT(N'TenantId') AS int) FOR TenantId 
GO

ALTER TABLE Posts     
    ADD CONSTRAINT df_TenantId_Posts      
    DEFAULT CAST(SESSION_CONTEXT(N'TenantId') AS int) FOR TenantId 
GO 
```

Ahora aplicación hello no es necesario un valor de TenantId toospecify al insertar filas: 

```
SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() => 
{   
    using (var db = new ElasticScaleContext<int>(sharding.ShardMap, tenantId, connStrBldr.ConnectionString))
    {
        var blog = new Blog { Name = name }; // default constraint sets TenantId automatically     
        db.Blogs.Add(blog);     
        db.SaveChanges();   
    } 
}); 
```

> [!NOTE]
> Si utiliza las restricciones predeterminadas de un proyecto de Entity Framework, se recomienda que no incluye columnas de TenantId de hello en el modelo de datos EF. Esto es porque las consultas de Entity Framework proporcionan automáticamente los valores predeterminados que invalidarán Hola predeterminado las restricciones creadas en T-SQL que utilizan SESSION_CONTEXT. proyecto de ejemplo de las restricciones predeterminadas de toouse en hello, por ejemplo, debes quitar TenantId DataClasses.cs (y Add-Migration ejecución en la consola de administrador de paquetes de saludo) y tooensure usar T-SQL que Hola campo solo se encuentra en tablas de base de datos de Hola. De este modo, EF no proporcionará automáticamente los valores predeterminados incorrectos al insertar datos. 
> 
> 

### <a name="optional-enable-a-superuser-tooaccess-all-rows"></a>(Opcional) Habilitar todas las filas de una tooaccess de "superusuario"
Algunas aplicaciones pueden necesitar toocreate "superusuario" quién puede acceder a todas las filas, por ejemplo, en tooenable orden reporting a través de todos los inquilinos en todas las particiones o las operaciones de división/combinación tooperform en particiones que implican mover filas de inquilino entre bases de datos. tooenable esto, debe crear un nuevo usuario SQL ("superusuario" en este ejemplo) en cada base de datos de la partición. A continuación, modifique la directiva de seguridad de hello con una nueva función de predicado que permite a este usuario tooaccess todas las filas:

```
-- New predicate function that adds superuser logic
CREATE FUNCTION rls.fn_tenantAccessPredicateWithSuperUser(@TenantId int)
    RETURNS TABLE
    WITH SCHEMABINDING
AS
    RETURN SELECT 1 AS fn_accessResult 
        WHERE 
        (
            DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('dbo') -- note, should not be dbo!
            AND CAST(SESSION_CONTEXT(N'TenantId') AS int) = @TenantId
        ) 
        OR
        (
            DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('superuser')
        )
GO

-- Atomically swap in hello new predicate function on each table
ALTER SECURITY POLICY rls.tenantAccessPolicy
    ALTER FILTER PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Blogs,
    ALTER BLOCK PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Blogs,
    ALTER FILTER PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Posts,
    ALTER BLOCK PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Posts
GO
```


### <a name="maintenance"></a>Mantenimiento
* **Agregar nuevas particiones**: debe ejecutar script de Hola T-SQL tooenable RLS en las nuevas particiones, en caso contrario, no se filtrarán las consultas en esas particiones.
* **Adición de nuevas tablas**: debe agregar un filtro y bloquear la directiva de seguridad de predicado toohello en todas las particiones siempre que se crea una nueva tabla, en caso contrario, no se filtrarán las consultas en la nueva tabla de Hola. Esto se puede automatizar mediante un desencadenador DDL, como se describe en [aplicar seguridad de nivel de fila toonewly crea automáticamente tablas (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/22/apply-row-level-security-automatically-to-newly-created-tables.aspx).

## <a name="summary"></a>Resumen
Herramientas de bases de datos elásticas y seguridad de nivel de fila pueden ser usado tooscale junto a la capa de datos de una aplicación con compatibilidad para varios inquilinos y único inquilino particiones. Particiones de varios inquilinos pueden ser utilizados toostore datos más eficazmente (especialmente en casos donde un gran número de los inquilinos tener solamente algunas filas de datos), al único inquilino particiones pueden ser los inquilinos de premium toosupport usados con más estrictos aislamiento y rendimiento requisitos.  Para obtener más información, consulte la [referencia sobre la seguridad de nivel de fila](https://msdn.microsoft.com/library/dn765131). 

## <a name="additional-resources"></a>Recursos adicionales
* [¿Qué es un grupo elástico de Azure?](sql-database-elastic-pool.md)
* [Escalado horizontal con Base de datos SQL de Azure](sql-database-elastic-scale-introduction.md)
* [Modelos de diseño para las aplicaciones SaaS multiinquilino con base de datos SQL de Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* [Authentication in multitenant apps, using Azure AD and OpenID Connect](../guidance/guidance-multitenant-identity-authenticate.md)
* [Aplicación Tailspin Surveys](../guidance/guidance-multitenant-identity-tailspin.md)

## <a name="questions-and-feature-requests"></a>Preguntas y solicitudes de características
Si tiene preguntas, póngase en contacto toous en hello [foro de base de datos SQL](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) y para las solicitudes de características, agréguelos toohello [foro de comentarios de la base de datos SQL](https://feedback.azure.com/forums/217321-sql-database/).

<!--Image references-->
[1]: ./media/sql-database-elastic-tools-multi-tenant-row-level-security/blogging-app.png
<!--anchors-->


