---
title: aaaGranting acceso tooAzure base de datos SQL | Documentos de Microsoft
description: "Obtenga información acerca de cómo conceder acceso tooMicrosoft base de datos de SQL Azure."
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 8e71b04c-bc38-4153-8f83-f2b14faa31d9
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 02/06/2017
ms.author: rickbyh
ms.openlocfilehash: 4c32fafa7e98b731ff2f9bf4666da7e4a3145286
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-access-control"></a>Control de acceso a Azure SQL Database
seguridad tooprovide, base de datos SQL controla el acceso con reglas de firewall limitar conectividad por dirección IP, los mecanismos de autenticación que requieren los usuarios tooprove su identidad, mecanismos de autorización y limitar las acciones de toospecific de los usuarios y los datos. 

> [!IMPORTANT]
> Para obtener información general de las características de seguridad de base de datos SQL de hello, consulte [información general de seguridad SQL](sql-database-security-overview.md). Para ver un tutorial, consulte [Protección de Azure SQL Database](sql-database-security-tutorial.md).

## <a name="firewall-and-firewall-rules"></a>Firewall y reglas de firewall
Microsoft Azure SQL Database ofrece un servicio de base de datos relacional para Azure y otras aplicaciones basadas en Internet. toohelp proteger los datos, firewalls impedir que todos los servidores de base de datos de access tooyour hasta que especifique qué equipos tienen permiso. firewall de Hello otorga toodatabases de acceso basado en hello procedentes de la dirección IP de cada solicitud. Para más información, consulte [Introducción a las reglas de firewall de Azure SQL Database](sql-database-firewall-configure.md).

Hola servicio de base de datos de SQL Azure solo está disponible a través del puerto TCP 1433. tooaccess una base de datos de SQL desde el equipo, asegúrese de que el firewall del equipo cliente permite la comunicación de TCP de salida en el puerto TCP 1433. Si no es necesario para otras aplicaciones, bloquee las conexiones entrantes en el puerto TCP 1433. 

Como parte del proceso de conexión de hello, conexiones de máquinas virtuales de Azure son tooa redirigida otra dirección IP y el puerto, único para cada rol de trabajador. número de puerto de Hello es en el intervalo de hello entre too11999 11000. Para obtener más información sobre los puertos TCP, consulte [Puertos más allá del 1433 para ADO.NET 4.5 y SQL Database2](sql-database-develop-direct-route-ports-adonet-v12.md).

## <a name="authentication"></a>Autenticación

Base de datos SQL admite dos tipos de autenticación:

* **Autenticación de SQL**, que usa un nombre de usuario y una contraseña. Cuando crea el servidor lógico de hello para la base de datos, especificar un inicio de sesión de "administrador del servidor" con un nombre de usuario y una contraseña. Con estas credenciales, puede autenticar tooany base de datos en ese servidor como propietario de la base de datos de Hola o "dbo". 
* **Autenticación de Azure Active Directory**, que usa las identidades administradas por Azure Active Directory y es compatible con dominios administrados e integrados. Use la autenticación de Active Directory (seguridad integrada) [siempre que sea posible](https://docs.microsoft.com/sql/relational-databases/security/choose-an-authentication-mode). Si desea toouse autenticación de Azure Active Directory, debe crear otro administrador de servidor llamado hello "Azure AD admin", que se permite grupos y usuarios de Azure AD tooadminister. Este administrador también puede realizar todas las operaciones de un administrador de servidor normal. Vea [conectar tooSQL base de datos mediante Active Directory autenticación de Azure](sql-database-aad-authentication.md) para ver un tutorial sobre cómo toocreate una tooenable de administración de Azure AD autenticación de Azure Active Directory.

Hola motor de base de datos cierra la conexión que permanezca inactivo durante más de 30 minutos. Hola conexión debe volver a iniciar sesión antes de poder utilizarlo. Continuamente las conexiones activas tooSQL base de datos requieren vuelva a autorizarla (lo realiza el motor de base de datos de hello) al menos cada 10 horas. motor de base de datos de Hello intenta vuelva a autorizarla con contraseña enviada originalmente hello y no proporcionados por el usuario es obligatorio. Por motivos de rendimiento cuando se restablece una contraseña de base de datos de SQL, Hola conexión no es puede volver a autenticar, incluso si se restablece la conexión de hello debido tooconnection agrupación. Esto es diferente del comportamiento de Hola de local de SQL Server. Si se ha cambiado la contraseña de hello puesto que inicialmente se ha autorizado la conexión de hello, debe terminar la conexión de Hola y establece una nueva conexión con hello nueva contraseña. Un usuario con hello `KILL DATABASE CONNECTION` permiso puede finalizar explícitamente una base de datos de conexión tooSQL utilizando hello [KILL](https://docs.microsoft.com/sql/t-sql/language-elements/kill-transact-sql) comando.

Cuentas de usuario pueden crearse en la base de datos maestra de Hola y se pueden conceder permisos en todas las bases de datos en el servidor de hello, o se pueden crear en hello propia base de datos (denominados usuarios contenidos). Para más información sobre cómo crear y administrar inicios de sesión, consulte [Administración de inicios de sesión](sql-database-manage-logins.md). portabilidad de tooenhance y escalabilidad, utilice escalabilidad de tooenhance de usuarios de base de datos independiente. Para más información sobre los usuarios de bases de datos independientes, consulte [Usuarios de bases de datos independientes: llévense sus bases de datos donde quieran](https://docs.microsoft.com/sql/relational-databases/security/contained-database-users-making-your-database-portable), [CREATE USER (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/create-user-transact-sql) y [Bases de datos independientes](https://docs.microsoft.com/sql/relational-databases/databases/contained-databases).

Como práctica recomendada de su aplicación debe utilizar un tooauthenticate cuenta dedicada: este modo puede limitar los permisos de hello concedidos toohello aplicación y reducir los riesgos de Hola de actividad malintencionada en caso de que el código de aplicación es vulnerable tooa inyección de código SQL ataque. Hola recomendado consiste toocreate una [usuario de base de datos independiente](https://docs.microsoft.com/sql/relational-databases/security/contained-database-users-making-your-database-portable), lo que permite la aplicación tooauthenticate directamente toohello base de datos. 

## <a name="authorization"></a>Autorización

La autorización refiere toowhat puede hacer un usuario dentro de una base de datos de SQL Azure, y esto se controla mediante la base de datos de su cuenta de usuario [las pertenencias a roles](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/database-level-roles) y [permisos de nivel de objeto](https://docs.microsoft.com/sql/relational-databases/security/permissions-database-engine). Como práctica recomendada, debe conceder Hola usuarios privilegios mínimos necesarios. cuenta de administrador de servidor de saludo con que se está conectando es un miembro de db_owner, que tiene autoridad toodo cualquier elemento dentro de la base de datos de Hola. Guarde esta cuenta para implementar las actualizaciones de los esquemas y otras operaciones de administración. Usar cuenta de "ApplicationUser" hello con más limitada tooconnect de permisos de la base de datos de aplicación toohello con hello privilegios mínimos necesarios para la aplicación. Para más información, consulte [Administración de inicios de sesión](sql-database-manage-logins.md).

Normalmente, sólo los administradores necesitan acceder a toohello `master` base de datos. Debe ser la base de datos de usuario de acceso rutinario tooeach a través de los usuarios de base de datos independiente sin privilegios de administrador creados en cada base de datos. Al usar los usuarios de base de datos independiente, no es necesario toocreate los inicios de sesión en hello `master` base de datos. Para obtener más información, vea [Usuarios de base de datos independiente - Conversión de la base de datos en portátil](https://docs.microsoft.com/sql/relational-databases/security/contained-database-users-making-your-database-portable).

Debe familiarizarse con hello después de características que pueden ser usado toolimit o elevar los permisos:   
* [Suplantación](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/customizing-permissions-with-impersonation-in-sql-server) y [la firma de módulos](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/signing-stored-procedures-in-sql-server) puede ser usado toosecurely elevar permisos temporalmente.
* [seguridad del nivel de fila](https://docs.microsoft.com/sql/relational-databases/security/row-level-security) permite filtrar las filas que puede ver el usuario.
* [El enmascaramiento de datos](sql-database-dynamic-data-masking-get-started.md) puede ser usado toolimit la exposición de información confidencial.
* [Procedimientos almacenados](https://docs.microsoft.com/sql/relational-databases/stored-procedures/stored-procedures-database-engine) puede ser usado toolimit acciones de Hola que pueden realizarse en la base de datos de Hola.

## <a name="next-steps"></a>Pasos siguientes

- Para obtener información general de las características de seguridad de base de datos SQL de hello, consulte [información general de seguridad SQL](sql-database-security-overview.md).
- toolearn más información acerca de las reglas de firewall, consulte [las reglas de Firewall](sql-database-firewall-configure.md).
- toolearn acerca de los usuarios e inicios de sesión, vea [administrar inicios de sesión](sql-database-manage-logins.md). 
- Para analizar la supervisión proactiva, consulte [Auditorías de SQL Database](sql-database-auditing.md) y [Detección de amenazas de SQL Database](sql-database-threat-detection.md).
- Para ver un tutorial, consulte [Protección de Azure SQL Database](sql-database-security-tutorial.md).
