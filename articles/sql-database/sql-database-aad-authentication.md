---
title: "autenticación de Active Directory aaaAzure - SQL de Azure (Introducción) | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Azure Active Directory para la autenticación con la base de datos SQL y almacenamiento de datos de SQL"
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 7e2508a1-347e-4f15-b060-d46602c5ce7e
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 08/11/2017
ms.author: rickbyh
ms.openlocfilehash: 7a63a162653b65294e11d3fa5bf39c320e742854
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-active-directory-authentication-for-authentication-with-sql-database-or-sql-data-warehouse"></a>Uso de la autenticación de Azure Active Directory con SQL Database o SQL Data Warehouse
La autenticación de Azure Active Directory es un mecanismo de conexión tooMicrosoft base de datos de SQL Azure y [almacenamiento de datos SQL](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) mediante el uso de identidades en Azure Active Directory (Azure AD). Con la autenticación de Azure AD, puede administrar de forma centralizada las identidades de Hola de usuarios de base de datos y otros servicios de Microsoft en una ubicación central. Administración del identificador central proporciona un único lugar a los usuarios de base de datos de toomanage y simplifica la administración de permisos. Ventajas Hola siguientes:

* Proporciona una autenticación de servidor alternativo tooSQL.
* Ayuda a detener la proliferación de Hola de identidades de usuario entre los servidores de base de datos.
* Permite la rotación de contraseñas en un solo lugar
* Los clientes pueden administrar los permisos de la base de datos con grupos externos (AAD).
* Puede eliminar el almacenamiento de contraseñas mediante la habilitación de la autenticación integrada de Windows y otras formas de autenticación compatibles con Azure Active Directory.
* Autenticación de Azure AD utiliza las identidades de tooauthenticate de usuarios de base de datos independiente en el nivel de base de datos de Hola.
* Azure AD admite autenticación basada en el símbolo (token) para aplicaciones que se conectan tooSQL base de datos.
* La autenticación de Azure AD es compatible con ADFS (federación de dominio) o la autenticación nativa de usuario y contraseña para una instancia de Azure Active Directory local sin sincronización de dominios.  
* Azure AD admite conexiones de SQL Server Management Studio que usan la autenticación universal de Active Directory, lo cual incluye Multi-Factor Authentication (MFA).  MFA incluye una sólida autenticación con una gama de sencillas opciones de comprobación: llamada de teléfono, mensaje de texto, tarjetas inteligentes con PIN o notificación de aplicación móvil. Para obtener más información, consulte [Compatibilidad de SSMS con Azure AD MFA con Base de datos SQL y Almacenamiento de datos SQL](sql-database-ssms-mfa-authentication.md).  

>  [!NOTE]  
>  Conexión tooSQL servidor se ejecuta en una VM de Azure no es compatible con una cuenta de Azure Active Directory. Utilice en su lugar una cuenta de Active Directory del dominio.  

pasos de configuración de Hello incluyen hello siguiendo los procedimientos tooconfigure y utilice autenticación de Azure Active Directory.

1. Cree y rellene una instancia de Azure AD.
2. Opcional: Asociar o cambiar Hola active directory que está asociada actualmente con la suscripción de Azure.
3. Cree un administrador de Azure Active Directory para Azure SQL Server o para [Azure SQL Data Warehouse](https://azure.microsoft.com/services/sql-data-warehouse/).
4. Configure los equipos cliente.
5. Crear usuarios de base de datos independiente en la base de datos asignado tooAzure identidades de AD.
6. Conectar la base de datos de tooyour mediante el uso de identidades de Azure AD.

> [!NOTE]
> toolearn cómo toocreate y rellenar Azure AD y, a continuación, configurar Azure AD con la base de datos de SQL Azure y almacenamiento de datos de SQL, consulte [configurar Azure AD con la base de datos de SQL Azure](sql-database-aad-authentication-configure.md).
>

## <a name="trust-architecture"></a>Arquitectura de confianza
Hola después de diagrama de alto nivel resume la arquitectura de la solución de Hola de utilizar autenticación de Azure AD con base de datos de SQL Azure. Hello mismos conceptos aplican tooSQL almacenamiento de datos. se considera toosupport contraseña de usuario nativa de Azure AD, solo parte de la nube de Hola y base de datos de SQL Azure o SQL Azure AD. toosupport autenticación federada (o las credenciales de Windows de usuario/contraseña), se requiere comunicación Hola con bloque ADFS. las flechas de Hello indican las rutas de comunicación.

![diagrama de autenticación de aad][1]

Hello diagrama siguiente indica Hola federation, de confianza y relaciones que permiten a un cliente de base de datos de tooconnect tooa mediante el envío de un token de hospedaje. símbolo (token) de Hello es autenticado por Azure AD y es de confianza para la base de datos de Hola. El cliente 1 puede representar una instancia de Azure Active Directory con usuarios nativos o una instancia de AD con usuarios federados. El cliente 2 representa una posible solución, incluidos los usuarios importados; en este ejemplo proceden de una instancia de Azure Active Directory federada con ADFS sincronizado con Azure Active Directory. Es importante toounderstand que tienen acceso a la base de datos de tooa mediante autenticación de Azure AD requiere que Hola hospedaje suscripción esté asociado toohello Azure AD. Hello misma suscripción debe ser usado toocreate Hola SQL Server hospedaje Hola base de datos de SQL Azure o almacenamiento de datos SQL.

![relación de suscripción][2]

## <a name="administrator-structure"></a>Estructura del administrador
Cuando se usa autenticación de Azure AD, hay dos cuentas de administrador para el servidor de base de datos SQL de hello; Hola Administrador original de SQL Server y Administrador de hello Azure AD. Hello mismos conceptos aplican tooSQL almacenamiento de datos. Hola Administrador con permiso de acuerdo con una cuenta de Azure AD puede crear usuario de base de datos de Azure AD contenido primera hello en una base de datos de usuario. inicio de sesión de administrador de Hello Azure AD puede ser un usuario de Azure AD o un grupo de Azure AD. Cuando el Administrador de hello es una cuenta de grupo, se puede utilizar por cualquier miembro del grupo, lo que permite a varios administradores de Azure AD para la instancia de SQL Server de Hola. Con la cuenta de grupo como un administrador mejora la facilidad de uso al permitir toocentrally agregar y quitar miembros del grupo en Azure AD sin cambiar los usuarios de Hola o permisos de base de datos de SQL. Solo un administrador de Azure AD (un usuario o grupo) se puede configurar en cualquier momento.

![estructura de administración][3]

## <a name="permissions"></a>Permisos
toocreate nuevos usuarios, debe tener hello `ALTER ANY USER` permiso de base de datos de Hola. Hola `ALTER ANY USER` permiso se puede conceder tooany usuario de base de datos. Hola `ALTER ANY USER` permiso también se mantiene en las cuentas de administrador del servidor de Hola y usuarios de base de datos con hello `CONTROL ON DATABASE` o `ALTER ON DATABASE` permiso para esa base de datos y los miembros de hello `db_owner` rol de base de datos.

toocreate un usuario de base de datos independiente en la base de datos de SQL Azure o almacenamiento de datos SQL, debe conectarse con una identidad de Azure AD de base de datos de toohello. usuario toocreate Hola primera base de datos independiente, debe conectarse toohello base de datos mediante el uso de un administrador de Azure AD (que es propietario de Hola de base de datos de hello). Esto se muestra a continuación, en los pasos 4 y 5. Cualquier autenticación de Azure AD solo es posible si Hola, Administrador de Azure AD se creó para la base de datos de SQL Azure y almacenamiento de datos de SQL server. Si se quitó Hola, Administrador de Azure Active Directory del servidor de hello, los usuarios existentes de Azure Active Directory que creó anteriormente en SQL Server ya no pueden conectarse con sus credenciales de Azure Active Directory de base de datos de toohello.

## <a name="azure-ad-features-and-limitations"></a>Características y limitaciones de Azure AD
Hola después de los miembros de Azure AD se puede aprovisionar en Azure SQL server o de almacenamiento de datos SQL:

* Miembros nativo: un miembro creado en Azure AD en el dominio administrado de Hola o en un dominio de cliente. Para obtener más información, consulte [agregar su propios tooAzure de nombre de dominio AD](../active-directory/active-directory-add-domain.md).
* Miembros de dominio federado: un miembro creado en Azure AD con un dominio federado. Para más información, consulte [Microsoft Azure now supports federation with Windows Server Active Directory](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/)(Microsoft Azure ya admite la federación con Windows Server Active Directory).
* Miembros importados de otros directorios de Azure AD que son miembros nativos o miembros de dominio federado.
* Grupos de Active Directory creados como grupos de seguridad.

No se admiten las cuentas de Microsoft (por ejemplo, outlook.com, hotmail.com, live.com) ni otras cuentas de invitado (por ejemplo, gmail.com, yahoo.com). Si puede iniciar sesión demasiado[https://login.live.com](https://login.live.com) con contraseña o cuenta de hello, a continuación, usa una cuenta de Microsoft, que no se admite para la autenticación de Azure AD para la base de datos de SQL Azure o almacenamiento de datos de SQL Azure.

## <a name="connecting-using-azure-ad-identities"></a>Conexión mediante identidades de Azure AD

Autenticación de Azure Active Directory admite Hola siguientes métodos de conexión base de datos de tooa mediante identidades de Azure AD:

* Mediante la autenticación integrada de Windows.
* Mediante el nombre y contraseña de una entidad de seguridad de Azure AD
* Mediante la autenticación de token de aplicación

### <a name="additional-considerations"></a>Consideraciones adicionales

* capacidad de administración de tooenhance, se recomienda proporcionar un anuncio de Azure dedicado grupo como administrador.   
* Solo un administrador de Azure AD (un usuario o grupo) se puede configurar en un servidor de Azure SQL Server o Azure SQL Data Warehouse en cualquier momento.   
* Sólo un administrador de Azure AD para SQL Server puede conectarse inicialmente toohello servidor SQL de Azure o almacenamiento de datos de SQL Azure con una cuenta de Azure Active Directory. Administrador de Active Directory de Hello puede configurar posterior Azure AD a los usuarios de la base de datos.   
* Se recomienda establecer segundos de too30 de tiempo de espera de conexión de Hola.   
* SQL Server 2016 Management Studio y SQL Server Data Tools para Visual Studio 2015 (versión 14.0.60311.1 abril de 2016 o posterior) admiten la autenticación de Azure Active Directory. (Autenticación de azure AD es compatible con hello **proveedor de datos de .NET Framework para SqlServer**; por lo menos la versión 4.6 de .NET Framework). Hola, por tanto, las versiones más recientes de estas herramientas y aplicaciones de capa de datos (DAC y bacpac) pueden usar la autenticación de Azure AD.   
* [La versión 13.1 de ODBC](https://www.microsoft.com/download/details.aspx?id=53339) es compatible con la autenticación de Azure Active Directory; sin embargo, `bcp.exe` no se puede conectar mediante la autenticación de Azure Active Directory porque usa un proveedor de ODBC anterior.   
* `sqlcmd`es compatible con el principio de la autenticación de Azure Active Directory con versión 13.1 disponibles de Hola [centro de descarga de](http://go.microsoft.com/fwlink/?LinkID=825643).   
* SQL Server Data Tools para Visual Studio 2015 requiere al menos versión de abril de 2016 de Hola de hello Data Tools (versión 14.0.60311.1). Actualmente, los usuarios de Azure AD no se muestran en el explorador de objetos de SSDT. Como alternativa, ver los usuarios de hello en [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).   
* [Microsoft JDBC Driver 6.0 para SQL Server](https://www.microsoft.com/download/details.aspx?id=11774) es compatible con la autenticación de Azure AD. Consulte también [establecer propiedades de conexión de hello](https://msdn.microsoft.com/library/ms378988.aspx).   
* PolyBase no se puede autenticar mediante la autenticación de Azure AD.   
* Autenticación de Azure AD es compatible para la base de datos SQL con hello portal de Azure **Importar base de datos** y **exportar base de datos** hojas. Importación y exportación mediante autenticación de Azure AD también se admite desde Hola comando de PowerShell.   
* La autenticación de Azure AD se admite para SQL Database y SQL Data Warehouse mediante el uso de la CLI. Para obtener más información, consulte [Configuración y administración de la autenticación de Azure Active Directory con SQL Database o SQL Data Warehouse](sql-database-aad-authentication-configure.md) y [SQL Server - az sql server](https://docs.microsoft.com/en-us/cli/azure/sql/server).

## <a name="next-steps"></a>Pasos siguientes
- toolearn cómo toocreate y rellenar Azure AD y, a continuación, configurar Azure AD con la base de datos de SQL Azure o almacenamiento de datos de SQL Azure, consulte [configurar y administrar la autenticación de Azure Active Directory con la base de datos SQL o almacenamiento de datos de SQL](sql-database-aad-authentication-configure.md).
- Para obtener información general de acceso y control en SQL Database, consulte [Control de acceso a Azure SQL Database](sql-database-control-access.md).
- Para obtener información general de los inicios de sesión, usuarios y roles de base de datos de SQL Database, consulte [Control y concesión de acceso a bases de datos](sql-database-manage-logins.md).
- Para más información acerca de las entidades de seguridad de bases de datos, consulte [Entidades de seguridad](https://msdn.microsoft.com/library/ms181127.aspx).
- Para más información acerca de los roles de base de datos, consulte [Roles de nivel de base de datos](https://msdn.microsoft.com/library/ms189121.aspx).
- Para más información general acerca de las reglas de firewall de SQL Database, consulte [Introducción a las reglas de firewall de Azure SQL Database](sql-database-firewall-configure.md).

<!--Image references-->

[1]: ./media/sql-database-aad-authentication/1aad-auth-diagram.png
[2]: ./media/sql-database-aad-authentication/2subscription-relationship.png
[3]: ./media/sql-database-aad-authentication/3admin-structure.png
[4]: ./media/sql-database-aad-authentication/4select-subscription.png
[5]: ./media/sql-database-aad-authentication/5ad-settings-portal.png
[6]: ./media/sql-database-aad-authentication/6edit-directory-select.png
[7]: ./media/sql-database-aad-authentication/7edit-directory-confirm.png
[8]: ./media/sql-database-aad-authentication/8choose-ad.png
[9]: ./media/sql-database-aad-authentication/9ad-settings.png
[10]: ./media/sql-database-aad-authentication/10choose-admin.png
[11]: ./media/sql-database-aad-authentication/11connect-using-int-auth.png
[12]: ./media/sql-database-aad-authentication/12connect-using-pw-auth.png
[13]: ./media/sql-database-aad-authentication/13connect-to-db.png

