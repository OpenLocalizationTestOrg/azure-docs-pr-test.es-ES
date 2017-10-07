---
title: "aaaAzure SQL inicios de sesión y los usuarios | Documentos de Microsoft"
description: "Obtenga información acerca de la administración de seguridad de base de datos SQL, específicamente cómo toomanage base de datos seguridad de acceso y el inicio de sesión a través de la cuenta de entidad de seguridad de nivel de servidor de Hola."
keywords: "seguridad de la Base de datos SQL, administración de seguridad de la base de datos, seguridad de inicio de sesión, seguridad de la base de datos, acceso a la base de datos"
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 0a65a93f-d5dc-424b-a774-7ed62d996f8c
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 01/23/2017
ms.author: rickbyh
ms.openlocfilehash: dff889b9fed09146a10008c0d11ca9e71d91df5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="controlling-and-granting-database-access"></a>Control y concesión de acceso a bases de datos

Cuando se hayan configurado las reglas de firewall, personas pueden conectarse tooa base de datos SQL como una de las cuentas de administrador de hello, como propietario de la base de datos de Hola o como un usuario de base de datos en la base de datos de Hola.  

>  [!NOTE]  
>  En este tema se aplica tooAzure SQL server y tooboth base de datos SQL y almacenamiento de datos de SQL bases de datos que se crean en el servidor de SQL Azure Hola. Para simplificar, base de datos SQL se utiliza cuando se hace referencia tooboth base de datos SQL y almacenamiento de datos de SQL. 
>

> [!TIP]
> Para ver un tutorial, consulte [Protección de Azure SQL Database](sql-database-security-tutorial.md).
>


## <a name="unrestricted-administrative-accounts"></a>Cuentas administrativas sin restricciones
Hay dos cuentas administrativas (**administrador del servidor** y **administrador de Active Directory**) que actúan como administradores. tooidentify estas cuentas de administrador para SQL server, abra Hola portal de Azure y navegue toohello propiedades de SQL server.

![Administradores de SQL Server](./media/sql-database-manage-logins/sql-admins.png)

- **Administrador del servidor**   
Cuando se crea un servidor de Azure SQL, debe designar un **inicio de sesión de administrador del servidor**. SQL server crea esa cuenta como un inicio de sesión en la base de datos maestra Hola. Esta cuenta se conecta mediante la autenticación de SQL Server (nombre de usuario y contraseña). Solo puede existir una de estas cuentas.   
- **Administrador de Azure Active Directory**   
Una cuenta de Azure Active Directory, individual o una cuenta de grupo de seguridad, también se puede configurar como administrador. Es opcional tooconfigure Administrador de Azure AD, pero se debe configurar un administrador de Azure AD si desea toouse Azure AD cuentas tooconnect tooSQL base de datos. Para obtener más información acerca de cómo configurar el acceso a Azure Active Directory, vea [tooSQL de conexión base de datos o SQL datos almacenamiento mediante Azure Active Directory autenticación](sql-database-aad-authentication.md) y [SSMS compatibilidad con Azure AD MFA con SQL Base de datos y almacenamiento de datos SQL](sql-database-ssms-mfa-authentication.md).
 

Hola **administrador del servidor** y **administración de Azure AD** cuentas tiene Hola siguientes características:
- Estas son Hola únicas cuentas que pueden conectarse automáticamente tooany base de datos SQL en el servidor de Hola. (base de datos de usuario de tooa tooconnect, otras cuentas deben ser propietario de Hola Hola de base de datos, o tener una cuenta de usuario de base de datos de usuario de Hola.)
- Estas cuentas escriban bases de datos de usuario como hello `dbo` usuario y tienen todos los permisos de hello en bases de datos de usuario de Hola. (propietario Hola de una base de datos de usuario también incorporan a base de datos de hello como hello `dbo` usuario.) 
- Estas cuentas no escriba hello `master` base de datos como hello `dbo` usuario y tiene permisos en master limitados. 
- Estas cuentas no sean miembros de hello estándar de SQL Server `sysadmin` rol fijo de servidor que no está disponible en la base de datos SQL.  
- Pueden crear, modificar y quitar bases de datos, inicios de sesión, usuarios en la base de datos maestra y reglas de firewall de nivel de servidor.
- Estas cuentas pueden agregar y quitar miembros toohello `dbmanager` y `loginmanager` roles.
- Estas cuentas pueden ver hello `sys.sql_logins` tabla del sistema.

### <a name="configuring-hello-firewall"></a>Configuración de firewall de Hola
Cuando firewall de nivel de servidor hello está configurado para una dirección IP individual o un rango, Hola **administrador del servidor SQL** hello y **Administrador de Azure Active Directory** puede conectarse toohello base de datos maestra y Hola todos los en el caso de las bases de datos de usuario. firewall de nivel de servidor inicial de Hello puede configurarse a través de hello [portal de Azure](sql-database-get-started-portal.md)con [PowerShell](sql-database-get-started-powershell.md) o mediante hello [API de REST](https://msdn.microsoft.com/library/azure/dn505712.aspx). Una vez que se establece una conexión, también se pueden configurar otras reglas de firewall de nivel de servidor mediante [Transact-SQL](sql-database-configure-firewall-settings.md).

### <a name="administrator-access-path"></a>Ruta de acceso de administrador
Cuando firewall de nivel de servidor de hello esté configurado correctamente, Hola **administrador del servidor SQL** hello y **Administrador de Azure Active Directory** pueden conectarse utilizando herramientas de cliente como SQL Server Management Studio o SQL Herramientas de datos de servidor. Solo herramientas más recientes de hello proporcionan todas las características de Hola y capacidades. Hello siguiente diagrama muestra una configuración típica para hello dos cuentas de administrador.

![Ruta de acceso de administrador](./media/sql-database-manage-logins/1sql-db-administrator-access.png)

Cuando se usa un puerto abierto en el firewall de nivel de servidor hello, los administradores pueden conectarse tooany base de datos SQL.

### <a name="connecting-tooa-database-by-using-sql-server-management-studio"></a>Conexión tooa base de datos mediante SQL Server Management Studio
Para ver un tutorial de creación de un servidor, una base de datos, las reglas de firewall de nivel de servidor y utilizar tooquery una base de datos de SQL Server Management Studio, consulte [empezar a trabajar con servidores de base de datos de SQL Azure, las bases de datos y las reglas de firewall mediante el uso de hello portal de Azure y SQL Server Management Studio](sql-database-get-started-portal.md).

> [!IMPORTANT]
> Se recomienda que siempre utilice Hola versión más reciente de Management Studio tooremain sincronizada con actualizaciones tooMicrosoft Azure y base de datos SQL. [Actualice SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).


## <a name="additional-server-level-administrative-roles"></a>Roles administrativos de nivel de servidor adicionales
Además toohello administrativas roles de servidor que se ha descrito anteriormente, base de datos SQL exige en se pueden agregar dos funciones administrativas restringidas en cuentas de usuario de toowhich de base de datos maestra de Hola que conceda permisos tooeither crear bases de datos o administrar inicios de sesión.

### <a name="database-creators"></a>Creadores de bases de datos
Uno de estos roles administrativos es hello **dbmanager** rol. Los miembros de este rol pueden crear bases de datos nuevas. toouse este rol, cree un usuario en hello `master` la base de datos y, a continuación, agregue Hola usuario toohello **dbmanager** rol de base de datos. toocreate una base de datos, el usuario de hello debe ser un usuario en función de un inicio de sesión de SQL Server en la base de datos maestra de Hola o contenido de usuario de base de datos según un usuario de Azure Active Directory.

1. Toohello base de datos maestra se conecte mediante una cuenta de administrador.
2. Paso opcional: crear un inicio de sesión de autenticación de SQL Server, con hello [CREATE LOGIN](https://msdn.microsoft.com/library/ms189751.aspx) instrucción. Instrucción de ejemplo:
   
   ```
   CREATE LOGIN Mary WITH PASSWORD = '<strong_password>';
   ```
   
   > [!NOTE]
   > Al crear un inicio de sesión o un usuario de una base de datos independiente, use una contraseña segura. Para obtener más información, consulte [Contraseñas seguras](https://msdn.microsoft.com/library/ms161962.aspx).
    
   rendimiento de tooimprove, los inicios de sesión (entidades de seguridad de nivel de servidor) se almacenan temporalmente en caché en el nivel de base de datos de Hola. caché de autenticación de toorefresh hello, consulte [DBCC FLUSHAUTHCACHE](https://msdn.microsoft.com/library/mt627793.aspx).

3. En base de datos maestra de hello, cree un usuario mediante el uso de hello [CREATE USER](https://msdn.microsoft.com/library/ms173463.aspx) instrucción. Hola usuario puede ser usuario de base de datos de autenticación contenido Azure Active Directory (si ha configurado el entorno para la autenticación de Azure AD), o un usuario de base de datos de contenidos de la autenticación de SQL Server o un usuario de autenticación de SQL Server basándose en una instancia de SQL Inicio de sesión de autenticación de servidor (creado en el paso anterior de hello). Instrucciones de ejemplo:
   
   ```
   CREATE USER [mike@contoso.com] FROM EXTERNAL PROVIDER;
   CREATE USER Tran WITH PASSWORD = '<strong_password>';
   CREATE USER Mary FROM LOGIN Mary; 
   ```

4. Agregar nuevo usuario hello, toohello **dbmanager** rol de base de datos mediante el uso de hello [ALTER ROLE](https://msdn.microsoft.com/library/ms189775.aspx) instrucción. Instrucciones de ejemplo:
   
   ```
   ALTER ROLE dbmanager ADD MEMBER Mary; 
   ALTER ROLE dbmanager ADD MEMBER [mike@contoso.com];
   ```
   
   > [!NOTE]
   > Hola dbmanager es un rol de base de datos en la base de datos maestra por lo que solo puede agregar un rol de base de datos usuario toohello dbmanager. No se puede agregar un rol de nivel de toodatabase de inicio de sesión de nivel de servidor.
    
5. Si es necesario, configure un firewall regla tooallow Hola nuevo usuario tooconnect. (el nuevo usuario de hello puede estar cubierto por una regla de firewall existente).

Ahora el usuario Hola puede conectarse toohello base de datos maestra y puede crear nuevas bases de datos. cuenta de Hello crear base de datos de Hola se convierte en propietario de Hola de base de datos de Hola.

### <a name="login-managers"></a>Administradores de inicio de sesión
Hello otro rol administrativo sigue Hola rol de administrador de inicio de sesión. Miembros de este rol pueden crear nuevos inicios de sesión en base de datos maestra de Hola. Si lo desea, puede completar Hola los mismos pasos (crear un inicio de sesión y un usuario y agregar un usuario toohello **loginmanager** rol) tooenable un usuario toocreate nuevos inicios de sesión en master Hola. Normalmente los inicios de sesión no son necesarias cuando el nivel de base de datos de Microsoft recomienda utilizar usuarios de base de datos independiente, que se autentican en hello en lugar de usar los usuarios basados en inicios de sesión. Para obtener más información, vea [Usuarios de base de datos independiente - Conversión de la base de datos en portátil](https://msdn.microsoft.com/library/ff929188.aspx).

## <a name="non-administrator-users"></a>Usuarios no administradores
Por lo general, las cuentas sin privilegios de administrador no necesita acceder a toohello la base de datos maestra. Crear usuarios de base de datos independiente en nivel de base de datos de hello con hello [CREATE USER (Transact-SQL)](https://msdn.microsoft.com/library/ms173463.aspx) instrucción. Hola usuario puede ser usuario de base de datos de autenticación contenido Azure Active Directory (si ha configurado el entorno para la autenticación de Azure AD), o un usuario de base de datos de contenidos de la autenticación de SQL Server o un usuario de autenticación de SQL Server basándose en una instancia de SQL Inicio de sesión de autenticación de servidor (creado en el paso anterior de hello). Para obtener más información, vea [Usuarios de base de datos independiente - Conversión de la base de datos en portátil](https://msdn.microsoft.com/library/ff929188.aspx). 

usuarios de toocreate, conectar la base de datos toohello y ejecutar instrucciones toohello similares en los ejemplos siguientes:

```
CREATE USER Mary FROM LOGIN Mary; 
CREATE USER [mike@contoso.com] FROM EXTERNAL PROVIDER;
```

Inicialmente, solo uno de los administradores de Hola o propietario de Hola de base de datos de hello puede crear usuarios. usuarios nuevos de tooauthorize usuarios adicionales toocreate, conceder ese Hola de usuario seleccionado `ALTER ANY USER` permiso, mediante una instrucción como:

```
GRANT ALTER ANY USER tooMary;
```

control total de usuarios adicionales toogive de base de datos de hello, que sean miembro de hello **db_owner** rol fijo de base de datos mediante hello `ALTER ROLE` instrucción.

> [!NOTE]
> Hello más comunes motivo toocreate base de datos de usuarios en función de los inicios de sesión, es cuando tiene usuarios de autenticación de SQL Server que necesitan tener acceso a las bases de datos de toomultiple. Los usuarios basados en inicios de sesión son el inicio de sesión de toohello relacionados y sólo una contraseña que se mantiene para ese inicio de sesión. Los usuarios de base de datos independiente en bases de datos individuales son entidades individuales y cada uno mantiene su propia contraseña. Esto puede confundir a los usuarios de base de datos independiente si no mantienen sus contraseñas idénticas.

### <a name="configuring-hello-database-level-firewall"></a>Configuración de firewall de nivel de base de datos de Hola
Como práctica recomendada, los usuarios no administradores sólo deben tener acceso a través de bases de datos de la toohello de firewall de Hola que usan. En lugar de autorizar su IP direcciones a través de nivel de servidor hello de firewall y concederles acceso tooall bases de datos, usar hello [sp_set_database_firewall_rule](https://msdn.microsoft.com/library/dn270010.aspx) firewall de nivel de base de datos de instrucción tooconfigure Hola. no se puede configurar el firewall de nivel de base de datos de Hello mediante el portal de Hola.

### <a name="non-administrator-access-path"></a>Ruta de acceso de no administrador
Cuando firewall de nivel de base de datos de hello esté configurado correctamente, los usuarios de base de datos de hello pueden conectarse con herramientas de cliente como SQL Server Management Studio o SQL Server Data Tools. Solo herramientas más recientes de hello proporcionan todas las características de Hola y capacidades. Hola siguiente diagrama muestra una ruta de acceso de administrador no habitual.

![Ruta de acceso de no administrador](./media/sql-database-manage-logins/2sql-db-nonadmin-access.png)

## <a name="groups-and-roles"></a>Grupos y roles
Administración de acceso eficaz usa permisos asignados toogroups y roles en lugar de usuarios individuales. 

- Si utiliza la autenticación de Azure Active Directory, coloque los usuarios de Azure Active Directory en un grupo de Azure Active Directory. Cree un usuario de base de datos independiente para el grupo de Hola. Coloque uno o varios usuarios de base de datos en un [rol de base de datos](https://msdn.microsoft.com/library/ms189121) y, a continuación, asignar [permisos](https://msdn.microsoft.com/library/ms191291.aspx) toohello rol de base de datos.

- Al utilizar la autenticación de SQL Server, crear usuarios de base de datos independiente en la base de datos de Hola. Coloque uno o varios usuarios de base de datos en un [rol de base de datos](https://msdn.microsoft.com/library/ms189121) y, a continuación, asignar [permisos](https://msdn.microsoft.com/library/ms191291.aspx) toohello rol de base de datos.

roles de base de datos de Hello pueden ser funciones integradas de hello como **db_owner**, **db_ddladmin**, **db_datawriter**, **db_datareader**, **db_denydatawriter**, y **db_denydatareader**. **db_owner** es toogrant utilizadas permiso total tooonly unos pocos usuarios. Hello otros roles de base de datos son útiles para obtener rápidamente una base de datos simple en el desarrollo, pero no se recomiendan para la mayoría de las bases de datos de producción. Por ejemplo, hello **db_datareader** rol fijo de base de datos concede acceso de lectura tooevery tabla de base de datos de hello, que suele ser más de es estrictamente necesaria. Es mucho mejor hello toouse [CREATE ROLE](https://msdn.microsoft.com/library/ms187936.aspx) instrucción toocreate sus propios definidos por el usuario roles de base de datos y conceder cuidadosamente cada Hola rol permisos mínimos necesarios para las necesidades del negocio Hola. Cuando un usuario es miembro de varios roles, agregan permisos Hola de todos ellos.

## <a name="permissions"></a>Permisos
En Base de datos SQL, hay más de 100 permisos que pueden conceder o denegar individualmente. Muchos de estos permisos están anidados. Por ejemplo, hello `UPDATE` permiso sobre un esquema incluye hello `UPDATE` permiso en cada tabla dentro de ese esquema. Como en la mayoría de los sistemas de permiso, la denegación de Hola de un permiso invalida un permiso grant. Debido a la naturaleza Hola anidado y el número de Hola de permisos, puede tardar cuidado estudio toodesign una tooproperly de sistema de los permisos adecuados proteger la base de datos. Iniciar con lista de Hola de permisos en [permisos (motor de base de datos)](https://msdn.microsoft.com/library/ms191291.aspx) y revise hello [póster de tamaño](http://go.microsoft.com/fwlink/?LinkId=229142) de permisos de Hola.


### <a name="considerations-and-restrictions"></a>Consideraciones y restricciones
Al administrar inicios de sesión y los usuarios de base de datos SQL, tenga en cuenta Hola siguiente:

* Debe ser conectado toohello **maestro** base de datos al ejecutar hello `CREATE/ALTER/DROP DATABASE` instrucciones.   
* Hola toohello correspondiente del usuario de base de datos **administrador del servidor** inicio de sesión no se pueden modificar ni quitar. 
* Inglés de Estados Unidos es el idioma predeterminado de Hola de hello **administrador del servidor** inicio de sesión.
* Hola solo los administradores (**administrador del servidor** inicio de sesión o administrador de Azure AD) y los miembros de Hola de hello **dbmanager** rol de base de datos en hello **maestro** tiene la base de datos Hola de permiso tooexecute `CREATE DATABASE` y `DROP DATABASE` las instrucciones.
* Debe ser toohello conectado la base de datos maestra al ejecutar hello `CREATE/ALTER/DROP LOGIN` instrucciones. Sin embargo, el uso de inicios de sesión no es recomendable. En su lugar, utilice los usuarios de la base de datos independiente.
* base de datos de usuario de tooa tooconnect, debe proporcionar Hola nombre de base de datos de hello en la cadena de conexión de Hola.
* Hola solo los miembros principales de hello y de inicio de sesión de nivel de servidor de hello **loginmanager** rol de base de datos en hello **maestro** base de datos tiene Hola de permiso tooexecute `CREATE LOGIN`, `ALTER LOGIN`, y `DROP LOGIN` instrucciones.
* Al ejecutar hello `CREATE/ALTER/DROP LOGIN` y `CREATE/ALTER/DROP DATABASE` las instrucciones en una aplicación de ADO.NET, mediante comandos con parámetros no se permite. Para obtener más información, consulte [Comandos y parámetros](https://msdn.microsoft.com/library/ms254953.aspx).
* Al ejecutar hello `CREATE/ALTER/DROP DATABASE` y `CREATE/ALTER/DROP LOGIN` instrucciones, cada una de estas instrucciones debe ser Hola solo una instrucción en un lote de Transact-SQL. De lo contrario, se produce un error. Por ejemplo, hello que Transact-SQL siguiente comprueba si existe la base de datos de Hola. Si existe, un `DROP DATABASE` instrucción se denomina base de datos de tooremove Hola. Dado que hello `DROP DATABASE` instrucción no es Hola única instrucción en el lote de hello, ejecutando Hola siguiente instrucción Transact-SQL produce un error.

  ```
  IF EXISTS (SELECT [name]
           FROM   [sys].[databases]
           WHERE  [name] = N'database_name')
  DROP DATABASE [database_name];
  GO
  ```

* Al ejecutar hello `CREATE USER` instrucción con hello `FOR/FROM LOGIN` opción, debe ser Hola solo una instrucción en un lote de Transact-SQL.
* Al ejecutar hello `ALTER USER` instrucción con hello `WITH LOGIN` opción, debe ser Hola solo una instrucción en un lote de Transact-SQL.
* demasiado`CREATE/ALTER/DROP` un usuario requiere hello `ALTER ANY USER` permiso en la base de datos de Hola.
* Al propietario de Hola de un rol de base de datos intenta tooadd o quitar otro tooor de usuario de base de datos de la base de datos, se puede producir Hola siguiente error: **usuario o función 'Name' no existe en esta base de datos.** Este error se produce porque el usuario de hello no es propietario de toohello visible. tooresolve este problema, conceda Hola rol propietario Hola `VIEW DEFINITION` permiso de usuario de Hola. 


## <a name="next-steps"></a>Pasos siguientes

- toolearn más información acerca de las reglas de firewall, consulte [Firewall de base de datos de SQL Azure](sql-database-firewall-configure.md).
- Para obtener información general de todas las características de seguridad de base de datos SQL de hello, consulte [información general de seguridad SQL](sql-database-security-overview.md).
- Para ver un tutorial, consulte [Protección de Azure SQL Database](sql-database-security-tutorial.md).
- Para obtener información acerca de las vistas y los procedimientos almacenados, consulte [Creación de vistas y procedimientos almacenados](https://msdn.microsoft.com/library/ms365311.aspx)
- Para obtener información sobre la concesión de objeto de base de datos de access tooa, consulte [tooa de concesión de acceso a objetos de base de datos](https://msdn.microsoft.com/library/ms365327.aspx)
