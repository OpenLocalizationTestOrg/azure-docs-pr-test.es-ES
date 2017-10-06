---
title: "una base de datos en el almacén de datos de SQL aaaSecure | Documentos de Microsoft"
description: Sugerencias para proteger una base de datos en Almacenamiento de datos SQL de Azure para desarrollar soluciones.
services: sql-data-warehouse
documentationcenter: NA
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: 8fa2f5ca-4cf5-4418-99a2-4dc745799850
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 5ef4d760e00be46bfe7808bc95dbe1e4b3a51165
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-database-in-sql-data-warehouse"></a>Proteger una base de datos en Almacenamiento de datos SQL
> [!div class="op_single_selector"]
> * [Información general sobre seguridad](sql-data-warehouse-overview-manage-security.md)
> * [Autenticación](sql-data-warehouse-authentication.md)
> * [Cifrado (Portal)](sql-data-warehouse-encryption-tde.md)
> * [Cifrado (T-SQL)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

Este artículo le guía a través de los conceptos básicos de Hola de protección de la base de datos de almacenamiento de datos de SQL Azure. En concreto, este artículo le ayudará a empezar a trabajar con los recursos para limitar el acceso, proteger los datos y supervisar las actividades en una base de datos.

## <a name="connection-security"></a>Seguridad de conexión
Seguridad de conexión hace referencia toohow restringir y proteger las conexiones de base de datos tooyour con el cifrado de conexión y las reglas de firewall.

Las reglas de Firewall se utilizan por ambos Hola hello y servidor de base de datos tooreject intentos de conexión desde direcciones IP que no han sido explícitamente en la lista blanca. tooallow las conexiones de la aplicación o la dirección IP pública del equipo cliente, primero debe crear una regla de firewall de nivel de servidor mediante Hola Portal de Azure, API de REST o PowerShell. Como práctica recomendada, debe restringir los intervalos de direcciones IP de hello permitidos a través del firewall de servidor tanto como sea posibles.  tooaccess almacenamiento de datos de SQL Azure desde el equipo local, asegúrese de firewall de hello en la red y el equipo local permita la comunicación saliente en el puerto TCP 1433.  Para obtener más información, consulte [Firewall de Azure SQL Database][Azure SQL Database firewall], [sp_set_firewall_rule][sp_set_firewall_rule] y [sp_set_database_firewall_rule][sp_set_database_firewall_rule].

Las conexiones tooyour almacenamiento de datos SQL se cifran de forma predeterminada.  Modificar toodisable de configuración de conexión se omiten el cifrado.

## <a name="authentication"></a>Autenticación
La autenticación refiere toohow demostrar su identidad cuando se conecta la base de datos de toohello. Actualmente, Almacenamiento de datos SQL admite la autenticación de SQL Server con un nombre de usuario y una contraseña, además de Azure Active Directory. 

Cuando crea el servidor lógico de hello para la base de datos, especificar un inicio de sesión de "administrador del servidor" con un nombre de usuario y una contraseña. Estas credenciales se puede autenticar tooany base de datos en ese servidor como propietario de la base de datos de Hola o "dbo" a través de la autenticación de SQL Server.

Sin embargo, como práctica recomendada, los usuarios de su organización deben usar una cuenta diferente tooauthenticate. De esta forma, puede limitar los permisos de hello concedidos toohello aplicación y reducir los riesgos de Hola de actividad malintencionada en caso de que el código de aplicación es vulnerable tooa ataque de inyección de SQL. 

toocreate un usuario autenticado de SQL Server, conecte toohello **maestro** en el servidor con su inicio de sesión de administrador del servidor de base de datos y crear un nuevo inicio de sesión de servidor.  Además, es un toocreate buena idea un usuario en la base de datos maestra de Hola para los usuarios de almacenamiento de datos de SQL Azure. La creación de un usuario en master permite un toologin de usuario con herramientas como SSMS sin especificar un nombre de base de datos.  También les permite toouse Hola objeto explorer tooview todas las bases de datos en un servidor SQL server.

```sql
-- Connect toomaster database and create a login
CREATE LOGIN ApplicationLogin WITH PASSWORD = 'Str0ng_password';
CREATE USER ApplicationUser FOR LOGIN ApplicationLogin;
```

A continuación, conecte tooyour **base de datos de almacenamiento de datos SQL** con su inicio de sesión de administrador del servidor y crear un usuario de base de datos en función de inicio de sesión de servidor de Hola que acaba de crear.

```sql
-- Connect tooSQL DW database and create a database user
CREATE USER ApplicationUser FOR LOGIN ApplicationLogin;
```

Si un usuario a realizar operaciones adicionales, como crear inicios de sesión o crear nuevas bases de datos, también necesitará toobe asignado toohello `Loginmanager` y `dbmanager` roles de base de datos maestra Hola. Para obtener más información sobre estas funciones adicionales y tooa autenticación de base de datos SQL, consulte [administrar bases de datos y los inicios de sesión en la base de datos de SQL Azure][Managing databases and logins in Azure SQL Database].  Para obtener más detalles sobre Azure AD para almacenamiento de datos SQL, consulte [conectar tooSQL datos almacenamiento mediante Active Directory autenticación de Azure][Connecting tooSQL Data Warehouse By Using Azure Active Directory Authentication].

## <a name="authorization"></a>Autorización
La autorización refiere toowhat que puede realizar en una base de datos de almacenamiento de datos de SQL Azure, y esto se controla mediante los permisos y pertenencias a roles de la cuenta de usuario. Como práctica recomendada, debe conceder Hola usuarios privilegios mínimos necesarios. Almacenamiento de datos de SQL Azure hace que esta toomanage fácil con roles de T-SQL:

```sql
EXEC sp_addrolemember 'db_datareader', 'ApplicationUser'; -- allows ApplicationUser tooread data
EXEC sp_addrolemember 'db_datawriter', 'ApplicationUser'; -- allows ApplicationUser toowrite data
```

cuenta de administrador de servidor de saludo con que se está conectando es un miembro de db_owner, que tiene autoridad toodo cualquier elemento dentro de la base de datos de Hola. Guarde esta cuenta para implementar las actualizaciones de los esquemas y otras operaciones de administración. Usar cuenta de "ApplicationUser" hello con más limitada tooconnect de permisos de la base de datos de aplicación toohello con hello privilegios mínimos necesarios para la aplicación.

Existen formas toofurther límite lo que un usuario puede hacer con la base de datos de SQL Azure:

* Granular [permisos] [ Permissions] permiten control qué operaciones puede en columnas individuales, tablas, vistas, procedimientos y otros objetos de base de datos de Hola. Use permisos granulares toohave Hola mayor control y otorgue Hola mínimos permisos necesarios. sistema de permisos granulares de Hello es complicado y requerirá algunos toouse práctico de forma eficaz.
* [Roles de base de datos] [ Database roles] distinto db_datareader y db_datawriter pueden ser usado toocreate menos eficaces cuentas de administración o cuentas de usuario de aplicación más eficaces. roles de base de datos fijos integrados de Hello proporcionan una manera sencilla los permisos toogrant, pero pueden dar lugar a conceder más permisos que son necesarios.
* [Procedimientos almacenados] [ Stored procedures] puede ser usado toolimit acciones de Hola que pueden realizarse en la base de datos de Hola.

Administrar bases de datos y servidores lógicos de hello Portal de Azure clásico o usar Hola API del Administrador de recursos de Azure se controla mediante asignaciones de roles de su cuenta de usuario del portal. Para obtener más información sobre este tema, consulte [Control de acceso basado en roles en Azure Portal][Role-based access control in Azure Portal].

## <a name="encryption"></a>Cifrado
Azure SQL datos de almacenamiento de datos cifrado transparente (TDE) ayuda a protegerse contra amenazas de Hola de actividad malintencionada mediante la realización de cifrado en tiempo real y el descifrado de los datos en reposo.  Al cifrar la base de datos, sin necesidad de las aplicaciones de tooyour de cambios se cifran los archivos de registro de transacciones y copias de seguridad asociadas. TDE cifra almacenamiento Hola de toda una base de datos mediante el uso de una clave de cifrado de base de datos de hello llamado de clave simétrica. En la base de datos SQL clave de cifrado de base de datos de hello está protegido por un certificado de servidor integrado. certificado de servidor integrado de Hello es único para cada servidor de base de datos SQL. Microsoft alterna automáticamente estos certificados al menos cada 90 días. algoritmo de cifrado de Hello usado por el almacenamiento de datos SQL es AES-256. Para ver una descripción general de TDE, consulte [Cifrado de datos transparente (TDE)][Transparent Data Encryption].

Puede cifrar la base de datos mediante hello [Portal de Azure] [ Encryption with Portal] o [T-SQL][Encryption with TSQL].

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información y ejemplos sobre la conexión tooyour almacenamiento de datos de SQL con diferentes protocolos, vea [conectar tooSQL Data Warehouse][Connect tooSQL Data Warehouse].

<!--Image references-->

<!--Article references-->
[Connect tooSQL Data Warehouse]: ./sql-data-warehouse-connect-overview.md
[Encryption with Portal]: ./sql-data-warehouse-encryption-tde.md
[Encryption with TSQL]: ./sql-data-warehouse-encryption-tde-tsql.md
[Connecting tooSQL Data Warehouse By Using Azure Active Directory Authentication]: ./sql-data-warehouse-authentication.md

<!--MSDN references-->
[Azure SQL Database firewall]: https://msdn.microsoft.com/library/ee621782.aspx
[sp_set_firewall_rule]: https://msdn.microsoft.com/library/dn270017.aspx
[sp_set_database_firewall_rule]: https://msdn.microsoft.com/library/dn270010.aspx
[Database roles]: https://msdn.microsoft.com/library/ms189121.aspx
[Managing databases and logins in Azure SQL Database]: https://msdn.microsoft.com/library/ee336235.aspx
[Permissions]: https://msdn.microsoft.com/library/ms191291.aspx
[Stored procedures]: https://msdn.microsoft.com/library/ms190782.aspx
[Transparent Data Encryption]: https://msdn.microsoft.com/library/bb934049.aspx
[Azure portal]: https://portal.azure.com/

<!--Other Web references-->
[Role-based access control in Azure Portal]: https://azure.microsoft.com/documentation/articles/role-based-access-control-configure
