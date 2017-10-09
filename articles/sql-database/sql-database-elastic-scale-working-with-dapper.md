---
title: "bibliotecas de cliente de base de datos elástica aaaUsing con Dapper | Documentos de Microsoft"
description: "Uso de la biblioteca de cliente de bases de datos elásticas con Dapper."
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: 463d2676-3b19-47c2-83df-f8c50492c9d2
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: c22ece2a977265e93850f0ad3f3ca48f0a8733ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-elastic-database-client-library-with-dapper"></a>Uso de la biblioteca de cliente de bases de datos elásticas con Dapper
Este documento va dirigido a desarrolladores que se basan en las aplicaciones de toobuild Dapper, pero también desea tooembrace [herramientas de base de datos elástica](sql-database-elastic-scale-introduction.md) toocreate aplicaciones que implementan el particionamiento horizontal tooscale su capa de datos.  Este documento ilustra cambios hello en aplicaciones basadas en Dapper que son necesario toointegrate con herramientas de base de datos elástica. Nuestro objetivo es en Redactar depende de los datos y de administración de particiones de bases de datos elásticas Hola enrutamiento con Dapper. 

**Código de ejemplo**: [Herramientas de bases de datos elásticas para Base de datos SQL de Azure: integración con Dapper](https://code.msdn.microsoft.com/Elastic-Scale-with-Azure-e19fc77f).

Integración de **Dapper** y **DapperExtensions** con hello biblioteca de cliente de base de datos elástica para base de datos de SQL Azure es fácil. Las aplicaciones pueden usar datos dependientes enrutamiento cambiando la creación de hello y abrir de nuevo [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) Hola de objetos toouse [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) llamar desde hello [cliente biblioteca](http://msdn.microsoft.com/library/azure/dn765902.aspx). Esto limita los cambios en su tooonly de aplicación donde se crea y se abre nuevas conexiones. 

## <a name="dapper-overview"></a>Información general sobre Dapper
**Dapper** es un asignador relacional de objetos. Se asigna a objetos de .NET desde la base de datos relacional tooa (y viceversa). primera parte de Hola Hola de código de ejemplo muestra cómo se puede integrar la biblioteca de cliente de base de datos elástica Hola con aplicaciones basadas en Dapper. segunda parte del código de ejemplo de Hola de Hello ilustra cómo toointegrate al usar Dapper y DapperExtensions.  

funcionalidad del asignador de Hello en Dapper proporciona métodos de extensión en las conexiones de base de datos que simplifican enviando instrucciones de T-SQL para la ejecución o la base de datos de consulta Hola. Por ejemplo, Dapper hace fácil toomap entre los objetos .NET y los parámetros de Hola de instrucciones SQL para **Execute** llamadas o los resultados de hello tooconsume de las consultas SQL en objetos de .NET mediante **consulta**llamadas desde Dapper. 

Al utilizar DapperExtensions, ya no necesita las instrucciones SQL de hello tooprovide. Métodos de extensión como **GetList** o **insertar** a través de la conexión de base de datos de hello crear Hola instrucciones SQL entre bastidores de Hola.

Otra ventaja de Dapper y también DapperExtensions es que los controles de aplicación Hola Hola creación de conexión de base de datos de Hola. Esto ayuda a interactuar con la biblioteca de cliente de base de datos elástica Hola que las conexiones según la asignación de Hola de shardlets toodatabases de base de datos de agentes.

ensamblados de tooget hello Dapper, consulte [Dapper punto net](http://www.nuget.org/packages/Dapper/). Hola Dapper de extensiones, vea [DapperExtensions](http://www.nuget.org/packages/DapperExtensions).

## <a name="a-quick-look-at-hello-elastic-database-client-library"></a>Un vistazo rápido a la biblioteca de cliente de base de datos elástica Hola
Con la biblioteca de cliente de base de datos elástica hello, para definir las particiones de los datos de aplicación denominado *shardlets* , asignarlos toodatabases e identificar por *claves de particionamiento*. Puede tener tantas bases de datos como necesite y distribuir los shardlets por dichas bases de datos. asignación de Hola de bases de datos de toohello de valores de clave de particionamiento se almacena mediante un mapa de particiones proporcionado por las API de la biblioteca de Hola. Esta funcionalidad se llama **administración de mapas de particiones**. mapa de particiones de Hello también actúa como broker Hola de conexiones de base de datos para las solicitudes que llevar a cabo una clave de particionamiento. Esta funcionalidad es que se hace referencia tooas **enrutamiento dependiente de datos**.

![Mapas de particiones y enrutamiento dependiente de los datos][1]

Administrador de mapa de particiones de Hello protege a los usuarios de vistas incoherentes en datos de shardlet que se pueden producir cuando se produzcan operaciones de administración de shardlet simultáneas en las bases de datos de Hola. toodo Hola por lo tanto, conexiones de base de datos de partición mapas broker Hola para una aplicación compilada con la biblioteca de Hola. Cuando las operaciones de administración de particiones podrían afectar a hello shardlet, esto permite kill de hello particiones mapa funcionalidad tooautomatically una conexión de base de datos. 

En lugar de utilizar las conexiones de toocreate de forma tradicional de Hola para Dapper, necesitamos hello toouse [OpenConnectionForKey método](http://msdn.microsoft.com/library/azure/dn824099.aspx). Esto garantiza que todas las validaciones de hello tiene lugar y las conexiones se administran correctamente cuando los datos se mueven entre las particiones.

### <a name="requirements-for-dapper-integration"></a>Requisitos para la integración de Dapper
Cuando se trabaja con la biblioteca de cliente de bases de datos elásticas de Hola y Hola API Dapper, queremos hello tooretain propiedades siguientes:

* **Ampliación**: se desea tooadd o quitar las bases de datos de capa de datos de Hola de aplicación particionada hello según sea necesario para las demandas de capacidad de Hola de aplicación hello. 
* **Coherencia**: puesto que nuestra aplicación es escalar horizontalmente mediante particionamiento, necesitamos enrutamiento dependiente de datos tooperform. Por lo que queremos toouse Hola datos dependientes capacidades de enrutamiento de hello biblioteca toodo. En concreto, queremos tooretain validación de Hola y proporcionan conexiones asíncronas a través del Administrador de mapa de particiones de hello en los resultados de consulta incorrecto o daños en orden tooavoid garantías de coherencia. Esto garantiza que ese tooa conexiones dado shardlet se rechazan o se detiene si (por ejemplo) hello shardlet tooa actualmente movida partición diferente mediante las API de dividir y combinar.
* **Asignación de objetos**: queremos comodidad de hello tooretain de asignaciones de hello proporcionada por Dapper tootranslate entre las clases de aplicación Hola y Hola subyacente estructuras de base de datos. 

Hello siguiente sección proporcionan instrucciones para estos requisitos para las aplicaciones basadas en **Dapper** y **DapperExtensions**.

## <a name="technical-guidance"></a>Orientación técnica
### <a name="data-dependent-routing-with-dapper"></a>Enrutamiento dependiente de los datos con Dapper
Con Dapper, la aplicación hello es suele ser responsable de crear y abrir Hola conexiones toohello subyacente de la base de datos. Dado un tipo T por aplicación hello, Dapper devuelve resultados de la consulta como colecciones de .NET de tipo T. Dapper realiza la asignación de Hola de hello T-SQL resultado filas toohello objetos de tipo T. De forma similar, Dapper asigna objetos .NET a valores de SQL o los parámetros de instrucciones de lenguaje (DML) de manipulación de datos. Dapper ofrece esta funcionalidad a través de métodos de extensión en hello regular [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) objeto desde bibliotecas de cliente de SQL de ADO .NET Hola. Hola conexión SQL devuelta por la API de escala elástica de Hola para DDR también son regular [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) objetos. Esto nos permite toodirectly utilizan Dapper extensiones sobre tipo hello devuelto por la API de DDR de la biblioteca de cliente de hello, ya que también es una simple conexión de cliente de SQL.

Estas observaciones facilitan conexiones toouse sencilla asíncronas biblioteca de cliente de base de datos elástica Hola para Dapper.

Este ejemplo de código (de Hola que acompaña a ejemplo) muestra enfoque de Hola donde proporciona clave de particionamiento de Hola Hola aplicación toohello biblioteca toobroker Hola conexión toohello derecho particiones.   

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                     key: tenantId1, 
                     connectionString: connStrBldr.ConnectionString, 
                     options: ConnectionOptions.Validate))
    {
        var blog = new Blog { Name = name };
        sqlconn.Execute(@"
                      INSERT INTO
                            Blog (Name)
                            VALUES (@name)", new { name = blog.Name }
                        );
    }

Hola llamada toohello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) API reemplaza creación predeterminada de Hola y apertura de una conexión de cliente de SQL. Hola [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) llamada toma argumentos de Hola que son necesarios para el enrutamiento dependiente de datos: 

* tooaccess de mapa de particiones de Hola Hola interfaces de enrutamiento dependiente de datos
* Hola particionamiento tooidentify clave hello shardlet
* partición de toohello tooconnect de Hello credenciales (nombre de usuario y contraseña)

objeto de mapa de particiones de Hello crea una partición de toohello de conexión que contiene shardlet Hola Hola clave de particionamiento dada. las API de cliente de base de datos elástica Hello también etiquetar Hola conexión tooimplement garantiza su coherencia. Desde Hola llamar demasiado[OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) devuelve un objeto regular de conexión de cliente de SQL, Hola llamada subsiguiente toohello **Execute** método de extensión de sigue Dapper Hola Dapper estándar práctica.

Consultas de trabajo muy Hola mismo forma - abrir por primera vez Hola conexión mediante [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) de API de cliente de Hola. A continuación, utilice Hola regular extensión Dapper métodos toomap Hola resultados de la consulta SQL en objetos .NET:

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId1, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate ))
    {    
           // Display all Blogs for tenant 1
           IEnumerable<Blog> result = sqlconn.Query<Blog>(@"
                                SELECT * 
                                FROM Blog
                                ORDER BY Name");

           Console.WriteLine("All blogs for tenant id {0}:", tenantId1);
           foreach (var item in result)
           {
                Console.WriteLine(item.Name);
            }
    }

Tenga en cuenta que hello **con** bloque con ámbitos de conexión de DDR de hello todas las operaciones de base de datos dentro de hello bloque toohello una partición que se conserva tenantId1. consulta de Hello solo devuelve blogs almacenados en la partición actual de hello, pero no Hola los almacenados en las otras particiones. 

## <a name="data-dependent-routing-with-dapper-and-dapperextensions"></a>Enrutamiento dependiente de datos con Dapper y DapperExtensions
Dapper incluye un ecosistema de extensiones adicionales que puede proporcionar más abstracción de base de datos de Hola y comodidad al desarrollar aplicaciones de base de datos. DapperExtensions es un ejemplo. 

El hecho de usar DapperExtensions en la aplicación no cambia la forma en que se crean y administran las conexiones de base de datos. Se esperan regulares objetos de conexión de cliente de SQL con métodos de extensión de Hola y sigue siendo tooopen conexiones de la aplicación hello responsabilidad. Podemos confiamos en hello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) tal y como se ha descrito anteriormente. Hola ejemplos de código siguientes muestran, Hola único cambio es que ya no tenemos las instrucciones de T-SQL Hola toowrite:

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId2, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate))
    {
           var blog = new Blog { Name = name2 };
           sqlconn.Insert(blog);
    }

Y este es el ejemplo de código de hello para consulta de hello: 

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId2, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate))
    {
           // Display all Blogs for tenant 2
           IEnumerable<Blog> result = sqlconn.GetList<Blog>();
           Console.WriteLine("All blogs for tenant id {0}:", tenantId2);
           foreach (var item in result)
           {
               Console.WriteLine(item.Name);
           }
    }

### <a name="handling-transient-faults"></a>Control de errores transitorios
Hello Microsoft Patterns & Practices equipo Hola publicado [Transient Fault Handling Application Block](http://msdn.microsoft.com/library/hh680934.aspx) los desarrolladores de aplicaciones de toohelp mitigar condiciones comunes de errores transitorios encontradas cuando se ejecuta en la nube de Hola. Para obtener más información, consulte [su perseverancia, secreto de todos los logros: mediante Hola Transient Fault Handling Application Block](http://msdn.microsoft.com/library/dn440719.aspx).

ejemplo de código de Hello se basa en hello errores transitorios biblioteca tooprotect frente a errores transitorios. 

    SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() =>
    {
       using (SqlConnection sqlconn = 
          shardingLayer.ShardMap.OpenConnectionForKey(tenantId2, connStrBldr.ConnectionString, ConnectionOptions.Validate))
          {
              var blog = new Blog { Name = name2 };
              sqlconn.Insert(blog);
          }
    });

**SqlDatabaseUtils.SqlRetryPolicy** en hello código anterior se define como un **SqlDatabaseTransientErrorDetectionStrategy** con un número de reintentos de 10 y 5 segundos de tiempo entre los reintentos de espera. Si está usando transacciones, asegúrese de que el ámbito de reintento vuelve toohello principio de la transacción de hello en caso de hello de un error transitorio.

## <a name="limitations"></a>Limitaciones
enfoques de Hola que se describen en este documento implican un par de limitaciones:

* código de ejemplo de Hola para este documento no se muestra cómo toomanage esquema entre las particiones.
* Dada una solicitud, se asume que todo el procesamiento de su base de datos está contenido en una sola partición identificada por la clave de particionamiento de hello proporcionada por solicitud de saludo. Sin embargo, esta suposición no siempre contener, por ejemplo, cuando no es posible toomake una clave de particionamiento disponible. tooaddress, Hola biblioteca de cliente de base de datos elástico incluye hello [MultiShardQuery clase](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardexception.aspx). clase Hello implementa una abstracción de conexión para las consultas en varias particiones. Uso de MultiShardQuery en combinación con Dapper es más allá del ámbito de Hola de este documento.

## <a name="conclusion"></a>Conclusión
Las aplicaciones que usan Dapper y DapperExtensions pueden beneficiarse fácilmente de las herramientas de bases de datos elásticas para Base de datos SQL de Azure. A través de hello pasos que se describen en este documento, esas aplicaciones pueden usar la capacidad de la herramienta de Hola para datos que dependen de enrutamiento cambiando la creación de hello y abrir de nuevo [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) hello toouse de objetos [ OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) llamada Hola elástico de base de datos de biblioteca de cliente. Esto limita toothose necesario lugares donde se crea y se abre nuevas conexiones de hello aplicación cambios. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-working-with-dapper/dapperimage1.png
