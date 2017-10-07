---
title: "credenciales de aaaManaging en la biblioteca de cliente de base de datos elástica Hola | Documentos de Microsoft"
description: "¿Cómo tooset Hola nivel adecuado de credenciales, administrador solo tooread, para las aplicaciones de base de datos elástica"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 72e0edaf-795e-4856-84a5-6594f735fb7e
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 218783ca2a07e3c0a4b089aa92634f32c41386e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="credentials-used-tooaccess-hello-elastic-database-client-library"></a>Credenciales usan la biblioteca de cliente de base de datos elástica tooaccess Hola
Hola [biblioteca de cliente de base de datos elástica](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) usa tres tipos diferentes de hello de credenciales tooaccess [manager de mapa de particiones](sql-database-elastic-scale-shard-map-management.md). Según la necesidad de hello, usar credenciales de Hola con un nivel más bajo de Hola de posibles de acceso.

* **Credenciales de administración**: se usan para crear o manipular un administrador de mapas de particiones. (Vea hello [glosario](sql-database-elastic-scale-glossary.md).) 
* **Las credenciales de acceso**: administrador tooobtain información acerca de particiones asignan tooaccess una partición existente.
* **Las credenciales de conexión**: tooconnect tooshards. 

Consulte, asimismo, [Administrar bases de datos e inicios de sesión en la Base de datos SQL de Azure](sql-database-manage-logins.md). 

## <a name="about-management-credentials"></a>Acerca de las credenciales de administración
Las credenciales de administración son toocreate usado un [ **ShardMapManager** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) objeto para las aplicaciones que manipulan mapas de particiones. (Por ejemplo, vea [agregar una partición con herramientas de base de datos elástica](sql-database-elastic-scale-add-a-shard.md) y [enrutamiento dependiente de datos](sql-database-elastic-scale-data-dependent-routing.md)) usuario Hola Hola escala elástica de biblioteca de cliente crea inicios de sesión SQL y los usuarios SQL de Hola y garantiza que cada uno de ellos se concede permisos de lectura/escritura de hello en particiones global Hola asignan base de datos y todas las bases de datos de particiones también. Estas credenciales son mapa de particiones global de Hola de toomaintain usado y mapas de particiones locales de hello cuando se realizan cambios mapa de particiones de toohello. Por ejemplo, usar Hola administración credenciales toocreate Hola particiones manager objeto map (mediante [ **GetSqlShardMapManager**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx): 

    // Obtain a shard map manager. 
    ShardMapManager shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager( 
            smmAdminConnectionString, 
            ShardMapManagerLoadPolicy.Lazy 
    ); 

variable de Hello **smmAdminConnectionString** es una cadena de conexión que contiene las credenciales de administración de Hola. Hola Id. de usuario y la contraseña proporciona base de datos de la asignación de particiones de lectura/escritura access tooboth y las particiones individuales. cadena de conexión de administración de Hello también incluye Hola servidor nombre y la base de datos nombre tooidentify Hola partición global mapa base de datos. Esta es una cadena de conexión típica para ese fin:

     "Server=<yourserver>.database.windows.net;Database=<yourdatabase>;User ID=<yourmgmtusername>;Password=<yourmgmtpassword>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;” 

No utilice valores en forma de Hola de "username@server", en su lugar, simplemente utilice el valor de "username" de Hola.  Esto es porque las credenciales deben funcionar con la base de datos de administrador de mapa de particiones de Hola y particiones individuales, que pueden estar en diferentes servidores.

## <a name="access-credentials"></a>Credenciales de acceso
Al crear una partición en el Administrador de asignación en una aplicación que no administrar asignaciones de particiones, utilice las credenciales que tienen permisos de solo lectura en el mapa de particiones global de Hola. Hello información recuperada de mapa de particiones global de hello en estas credenciales permiten [enrutamiento dependiente de los datos](sql-database-elastic-scale-data-dependent-routing.md) y partición de hello toopopulate asignar la memoria caché en el cliente de Hola. Hello las credenciales son proporcionados a través de hello mismo call (modelo) demasiado**GetSqlShardMapManager** como se indicó anteriormente: 

    // Obtain shard map manager. 
    ShardMapManager shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager( 
            smmReadOnlyConnectionString, 
            ShardMapManagerLoadPolicy.Lazy
    );  

Tenga en cuenta Hola uso del programa Hola a **smmReadOnlyConnectionString** tooreflect uso de Hola de credenciales diferentes para este acceso en nombre de **sin derechos administrativos** a los usuarios: estas credenciales no deberían proporcionar escritura permisos en el mapa de particiones global de Hola. 

## <a name="connection-credentials"></a>Credenciales de conexión
Se necesitan credenciales adicionales cuando se usa hello [ **OpenConnectionForKey** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx) método tooaccess una partición asociada a una clave de particionamiento. Estas credenciales necesitan permisos de tooprovide para tablas de mapas de acceso de solo lectura toohello particiones locales que residen en la partición de Hola. Se trata de validación de la conexión de tooperform necesarios para el enrutamiento dependiente de los datos en particiones de Hola. Este fragmento de código permite el acceso de datos en el contexto de Hola de enrutamiento dependiente de datos: 

    using (SqlConnection conn = rangeMap.OpenConnectionForKey<int>( 
    targetWarehouse, smmUserConnectionString, ConnectionOptions.Validate)) 

En este ejemplo, **smmUserConnectionString** contiene la cadena de conexión de Hola para hello las credenciales de usuario. En el caso de Base de datos SQL de Azure, la siguiente es una cadena de conexión típica para las credenciales de usuario: 

    "User ID=<yourusername>; Password=<youruserpassword>; Trusted_Connection=False; Encrypt=True; Connection Timeout=30;”  

Al igual que con las credenciales de administrador de hello, no los valores en forma de Hola de "username@server". En su lugar, use aquellos que tengan el formato "username".  Tenga en cuenta también que la cadena de conexión de hello no contiene un nombre de servidor y nombre de base de datos. Esto es así porque hello **OpenConnectionForKey** llamada dirigirá automáticamente Hola conexión toohello correcta de partición basada en clave de Hola. Por lo tanto, no se proporcionan el nombre de la base de datos de Hola y el nombre del servidor. 

## <a name="see-also"></a>Otras referencias
[Administrar bases de datos e inicios de sesión en Base de datos SQL de Azure](sql-database-manage-logins.md)

[Protección de bases de datos SQL](sql-database-security-overview.md)

[Introducción a Trabajos de base de datos elástica](sql-database-elastic-jobs-getting-started.md)

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

