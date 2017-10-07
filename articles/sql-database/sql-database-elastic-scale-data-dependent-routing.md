---
title: aaaData dependiente de enrutamiento con la base de datos de SQL de Azure | Documentos de Microsoft
description: "¿Cómo toouse Hola clase ShardMapManager en aplicaciones de .NET para el enrutamiento, una característica de bases de datos particionadas en base de datos de SQL Azure de dependiente de datos"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
editor: 
ms.assetid: cad09e15-5561-4448-aa18-b38f54cda004
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: ddove
ms.openlocfilehash: 34014508ae01905686791fe096bb275cb84f53b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="data-dependent-routing"></a>Enrutamiento dependiente de los datos
**Enrutamiento dependiente de datos** es Hola capacidad toouse Hola base de datos de una consulta tooroute Hola solicitud tooan adecuado. Se trata de un patrón fundamental cuando se trabaja con bases de datos particionadas. contexto de la solicitud de Hello también puede ser usado tooroute solicitud de hello, especialmente si clave de particionamiento de hello no forma parte de la consulta de Hola. Cada consulta específica o transacción en una aplicación con enrutamiento dependiente de datos está restringido tooaccessing una base de datos única por solicitud. Para las herramientas de hello elástico de base de datos de SQL de Azure, esta ruta se logra con hello  **[ShardMapManager clase](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)**  en aplicaciones de ADO.NET.

aplicación Hello no es necesario tootrack varias cadenas de conexión o ubicaciones de base de datos asociados a distintos segmentos de datos de entorno particionada Hola. En su lugar, Hola [Shard Map Manager](sql-database-elastic-scale-shard-map-management.md) abre las conexiones toohello correcta las bases de datos cuando sea necesario, en función de los datos de hello en mapa de particiones de Hola y el valor de Hola de clave de particionamiento de hello es destino de saludo de solicitud de la aplicación hello. Hola clave suele ser hello *customer_id*, *tenant_id*, *date_key*, o algún otro identificador específico que es un parámetro de solicitud de la base de datos de hello fundamental). 

Para más información, consulte [Scaling Out SQL Server with Data Dependent Routing](https://technet.microsoft.com/library/cc966448.aspx)(Escalado horizontal de SQL Server con enrutamiento dependiente de los datos).

## <a name="download-hello-client-library"></a>Descargar la biblioteca de cliente hello
clase de hello tooget, instalación hello [biblioteca de cliente de base de datos elástica](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/). 

## <a name="using-a-shardmapmanager-in-a-data-dependent-routing-application"></a>Usar un ShardMapManager en una aplicación de enrutamiento dependiente de datos
Las aplicaciones deben crear una instancia hello **ShardMapManager** durante la inicialización, mediante la llamada del generador de hello  **[GetSQLShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**. En este ejemplo, se inicializan **ShardMapManager** y un elemento **ShardMap** específico que contiene. En este ejemplo se muestra hello GetSqlShardMapManager y [GetRangeShardMap](https://msdn.microsoft.com/library/azure/dn824173.aspx) métodos.

    ShardMapManager smm = ShardMapManagerFactory.GetSqlShardMapManager(smmConnnectionString, 
                      ShardMapManagerLoadPolicy.Lazy);
    RangeShardMap<int> customerShardMap = smm.GetRangeShardMap<int>("customerMap"); 

### <a name="use-lowest-privilege-credentials-possible-for-getting-hello-shard-map"></a>Usar credenciales de privilegios más bajo posible para obtener el mapa de particiones de Hola
Si una aplicación no es la manipulación de propia asignación de particiones Hola, credenciales de hello utilizadas en el método de fábrica de hello deben tener permisos de solo de solo lectura en hello **Global mapa de particiones** base de datos. Estas credenciales son suelen ser diferentes de las credenciales usadas tooopen conexiones toohello particiones map manager. Vea también [credenciales usan la biblioteca de cliente de base de datos elástica tooaccess hello](sql-database-elastic-scale-manage-credentials.md). 

## <a name="call-hello-openconnectionforkey-method"></a>Llame al método de hello OpenConnectionForKey
Hola  **[ShardMap.OpenConnectionForKey método](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx)**  devuelve una conexión ADO.Net listo para la emisión de la base de datos de comandos toohello adecuada en función de valor de Hola de hello **clave**parámetro. Información de partición se almacena en memoria caché en la aplicación hello hello **ShardMapManager**, por lo que estas solicitudes no suelen implicar una búsqueda de base de datos contra Hola **Global mapa de particiones** base de datos. 

    // Syntax: 
    public SqlConnection OpenConnectionForKey<TKey>(
        TKey key,
        string connectionString,
        ConnectionOptions options
    )


* Hola **clave** parámetro se utiliza como clave de búsqueda en hello particiones mapa toodetermine Hola base de datos adecuada para la solicitud de Hola. 
* Hola **connectionString** son toopass utilizados solo credenciales de usuario de Hola para conexión de hello deseado. Ningún nombre de base de datos o el nombre del servidor se incluyen en este *connectionString* puesto que el método hello determinará la base de datos de Hola y servidor mediante hello **ShardMap**. 
* Hola  **[connectionOptions](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.connectionoptions.aspx)**  debe establecerse demasiado**ConnectionOptions.Validate** si puede cambiar un entorno donde partición se asigna y filas pueden mover bases de datos de tooother como un resultado de las operaciones de división o combinación. Esto implica un mapa de particiones local toohello breve consulta en la base de datos de destino hello (no en el mapa de toohello particiones global) antes de la conexión de Hola se entrega toohello aplicación. 

Si falla la validación de hello en mapa de particiones locales de hello (lo que indica que la memoria caché de hello es incorrecta), hello Shard Map Manager consultará Hola partición global mapa tooobtain Hola nuevo valor correcto para la búsqueda de hello, actualice su caché de hello y obtenga y devolver Hola conexión de base de datos correspondiente. 

Utilice **ConnectionOptions.None** solo cuando no se esperen cambios de asignación de particiones mientras una aplicación está en línea. En ese caso, valores de hello en caché pueden suponer tooalways sea correcta y se puede omitir sin ningún riesgo Hola validación de ida y vuelta adicional llamada toohello de datos de destino. Esto reduce el tráfico de la base de datos. Hola **connectionOptions** también se puede establecer a través de un valor en un tooindicate del archivo de configuración si se esperan que los cambios de particionamiento o no durante un período de tiempo.  

Este ejemplo usa el valor de Hola de una clave de entero **CustomerID**, utilizando un **ShardMap** objeto denominado **customerShardMap**.  

    int customerId = 12345; 
    int newPersonId = 4321; 

    // Connect toohello shard for that customer ID. No need toocall a SqlConnection 
    // constructor followed by hello Open method.
    using (SqlConnection conn = customerShardMap.OpenConnectionForKey(customerId, 
        Configuration.GetCredentialsConnectionString(), ConnectionOptions.Validate)) 
    { 
        // Execute a simple command. 
        SqlCommand cmd = conn.CreateCommand(); 
        cmd.CommandText = @"UPDATE Sales.Customer 
                            SET PersonID = @newPersonID 
                            WHERE CustomerID = @customerID"; 

        cmd.Parameters.AddWithValue("@customerID", customerId); 
        cmd.Parameters.AddWithValue("@newPersonID", newPersonId); 
        cmd.ExecuteNonQuery(); 
    }  

Hola **OpenConnectionForKey** método devuelve una nueva conexión ya abierto toohello base de datos correcta. Las conexiones utilizadas de esta manera seguirán aprovechando completamente las agrupaciones de conexiones de ADO.Net. Siempre y cuando las transacciones y las solicitudes se pueden lograr mediante una partición a la vez, debe ser única necesarios en una aplicación ya usa ADO.Net de modificación Hola. 

Hola  **[OpenConnectionForKeyAsync método](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkeyasync.aspx)**  también está disponible si la aplicación hace que la programación asincrónica de uso con ADO.Net. Su comportamiento es datos Hola dependientes enrutamiento equivalente de ADO. De NET  **[Connection.OpenAsync](https://msdn.microsoft.com/library/hh223688\(v=vs.110\).aspx)**  método.

## <a name="integrating-with-transient-fault-handling"></a>Integración con el control de errores transitorios
Una práctica recomendada para el desarrollo de aplicaciones de acceso a datos en la nube de hello es tooensure los errores transitorios se detecta la aplicación hello y que las operaciones de Hola se reintentan varias veces antes de producir un error. El control de errores transitorios para aplicaciones en la nube se describe en [Control de errores transitorios](https://msdn.microsoft.com/library/dn440719\(v=pandp.60\).aspx). 

Control de errores transitorios puede coexistir natural con el patrón de enrutamiento dependiente de datos Hola. Hola requisito clave es tooretry Hola solicitud de acceso de datos completo incluido hello **con** bloque que obtienen la conexión de enrutamiento dependiente de los datos de Hola. ejemplo de Hola anterior podría modificarse como sigue (Observe el cambio resaltado). 

### <a name="example---data-dependent-routing-with-transient-fault-handling"></a>Ejemplo: enrutamiento dependiente de los datos con control de errores transitorios
<pre><code>int customerId = 12345; 
int newPersonId = 4321; 

<span style="background-color:  #FFFF00">Configuration.SqlRetryPolicy.ExecuteAction(() =&gt; </span> 
<span style="background-color:  #FFFF00">    { </span>
        // Connect toohello shard for a customer ID. 
        using (SqlConnection conn = customerShardMap.OpenConnectionForKey(customerId,  
        Configuration.GetCredentialsConnectionString(), ConnectionOptions.Validate)) 
        { 
            // Execute a simple command 
            SqlCommand cmd = conn.CreateCommand(); 

            cmd.CommandText = @&quot;UPDATE Sales.Customer 
                            SET PersonID = @newPersonID 
                            WHERE CustomerID = @customerID&quot;; 

            cmd.Parameters.AddWithValue(&quot;@customerID&quot;, customerId); 
            cmd.Parameters.AddWithValue(&quot;@newPersonID&quot;, newPersonId); 
            cmd.ExecuteNonQuery(); 

            Console.WriteLine(&quot;Update completed&quot;); 
        } 
<span style="background-color:  #FFFF00">    }); </span> 
</code></pre>


Control de errores transitorios tooimplement necesarios son los paquetes descargan automáticamente cuando se crea la aplicación de ejemplo de Hola elástico de base de datos. Los paquetes también están disponibles por separado en [Biblioteca de información empresarial: bloque de aplicación Control de errores transitorios](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/). Use la versión 6.0 o posterior. 

## <a name="transactional-consistency"></a>Coherencia de las transacciones
Propiedades de transacción se garantiza para todas las particiones de tooa local de operaciones. Por ejemplo, las transacciones que se envían a través de enrutamiento dependiente de los datos se ejecuten dentro del ámbito de Hola de partición de destino de Hola de conexión de Hola. En este momento, no se proporcionan funcionalidades para alistar conexiones múltiples en una transacción y, por lo tanto, no hay garantías de transacciones para las operaciones realizadas a través de las particiones.

## <a name="next-steps"></a>Pasos siguientes
vea toodetach una partición o una partición, tooreattach [con los problemas de asignación de particiones de la clase toofix de hello RecoveryManager](sql-database-elastic-database-recovery-manager.md)

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

