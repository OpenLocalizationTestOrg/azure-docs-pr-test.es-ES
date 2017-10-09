---
title: "autenticación de Factor de aaaMulti - SQL de Azure | Documentos de Microsoft"
description: Use Multi-Factor Authentication con SSMS para SQL Database y SQL Data Warehouse.
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: fbd6e644-0520-439c-8304-2e4fb6d6eb91
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/19/2017
ms.author: rickbyh
ms.openlocfilehash: 57ef63b7c7f2c5cf64c3e1ee194d865ee5b14177
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="universal-authentication-with-sql-database-and-sql-data-warehouse-ssms-support-for-mfa"></a>Autenticación universal con SQL Database y SQL Data Warehouse (compatibilidad de SSMS con MFA)
Azure SQL Database y Azure SQL Data Warehouse admiten conexiones procedentes de SQL Server Management Studio (SSMS) mediante *Autenticación universal de Active Directory*. 
**Descargar SSMS más recientes de Hola** : en el equipo de cliente hello, descargar la versión más reciente de Hola de SSMS, desde [descargar SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx). Para todas las características de hello en este tema, utilice al menos de 2017 de julio, versión 17,2.  cuadro de diálogo de conexión más reciente Hello tiene este aspecto: ![1mfa-universal-conectar](./media/sql-database-ssms-mfa-auth/1mfa-universal-connect.png "cuadro de nombre de usuario de Hola se completa.")  

## <a name="hello-five-authentication-options"></a>Opciones de autenticación de Hello cinco  
- Autenticación Universal de Active Directory admite dos métodos de autenticación no interactiva hello (`Active Directory - Password` autenticación y `Active Directory - Integrated` autenticación). Los métodos de autenticación no interactivos `Active Directory - Password` y `Active Directory - Integrated` se pueden usar en muchas aplicaciones (ADO.NET, JDBC, ODBC, etc.). Estos dos métodos nunca generan cuadros de diálogo emergentes.

- La autenticación `Active Directory - Universal with MFA` es un método interactivo que también admite *Azure Multi-Factor Authentication* (MFA). Azure MFA ayuda a proteger acceso toodata y las aplicaciones al tiempo que satisface la demanda de los usuarios de un proceso de inicio de sesión simple. Ofrece una autenticación segura con una gama de opciones de comprobación sencilla (llamada de teléfono, mensaje de texto, las tarjetas inteligentes con pin o la notificación de aplicación móvil), lo cual permite un método de hello toochoose a los usuarios que prefieran. MFA interactivo con Azure AD puede generar un cuadro de diálogo emergente para la validación.

Para una descripción de Multi-Factor Authentication, consulte [Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md).
Para ver los pasos de configuración, consulte [Configure Azure SQL Database multi-factor authentication for SQL Server Management Studio](sql-database-ssms-mfa-authentication-configure.md) (Configuración de la autenticación multifactor de Azure SQL Database para SQL Server Management Studio).

### <a name="azure-ad-domain-name-or-tenant-id-parameter"></a>Nombre de dominio de Azure AD o parámetro de identificador de inquilino   

A partir de [SSMS versión 17](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), los usuarios que se importan en hello actual de Active Directory desde otros directorios de Azure Active Directory como usuarios invitados, puede proporcionar nombre de dominio de hello Azure AD, o identificador de inquilino cuando se conectan. Los usuarios invitados incluyen los que lo son desde otras instancias de Azure AD, cuentas de Microsoft como outlook.com, hotmail.com o live.com, u otras cuentas como gmail.com. Esta información permite **universales de Active Directory con la autenticación de MFA** tooidentify Hola correcto de autoridad de autenticación. Esta opción también es necesario toosupport cuentas de Microsoft (MSA), como outlook.com, hotmail.com, live.com o cuentas no son de MSA. Id. de todos estos usuarios que quieran toobe autenticado mediante la autenticación Universal debe escribir su nombre de dominio de Azure AD o inquilino. Este parámetro representa Hola de Id. de nombre/inquilino Hola actual de Azure AD dominio con que servidor Azure se vincula. Por ejemplo, si el servidor de Azure está asociado con el dominio de Azure AD `contosotest.onmicrosoft.com` donde usuario `joe@contosodev.onmicrosoft.com` está hospedado como un usuario de dominio de Azure AD importado `contosodev.onmicrosoft.com`, Hola tooauthenticate requerido un nombre de dominio este usuario es `contosotest.onmicrosoft.com`. Cuando el usuario de hello es un usuario de hello Azure AD vinculado tooAzure servidor nativo y no es una cuenta MSA, no es necesario ningún identificador de inquilino o el nombre de dominio. parámetro de hello tooenter (empezando por la versión 17,2 SSMS), en hello **conectar tooDatabase** cuadro de diálogo, cuadro de diálogo de hello completo, seleccionando **Active Directory - Universal con MFA** autenticación, Haga clic en **opciones**, Hola completa **nombre de usuario** cuadro y, a continuación, haga clic en hello **propiedades de conexión** ficha. Comprobar hello **identificador de inquilino o el nombre de dominio de AD** cuadro y proporcione la autoridad de autenticación, como nombre de dominio de hello (**contosotest.onmicrosoft.com**) u Hola GUID del identificador del inquilino Hola.  
   ![mfa-tenant-ssms](./media/sql-database-ssms-mfa-auth/mfa-tenant-ssms.png)   

### <a name="azure-ad-business-toobusiness-support"></a>Admitir toobusiness de negocio de Azure AD   
Usuarios de Azure AD admitidos escenarios B2B de Azure AD como usuarios invitados (vea [¿qué es la colaboración B2B de Azure](../active-directory/active-directory-b2b-what-is-azure-ad-b2b.md)) puede conectarse tooSQL base de datos y almacenamiento de datos de SQL únicamente como parte de los miembros de un grupo creado en Azure AD actual y asignar manualmente uso de Hola Transact-SQL `CREATE USER` instrucción en una base de datos. Por ejemplo, si `steve@gmail.com` es tooAzure invitado AD `contosotest` (con el dominio de Active Directory de Azure de hello `contosotest.onmicrosoft.com`), grupo de Azure AD, como `usergroup` debe crearse en Azure AD que contiene Hola Hola `steve@gmail.com` miembro. Después, el administrador de Azure AD SQL o un administrador de base de datos de Azure AD debe crear este grupo para una base de datos específica (por ejemplo, MyDatabase) ejecutando una instrucción `CREATE USER [usergroup] FROM EXTERNAL PROVIDER` de Transact-SQL. Después de crea el usuario de base de datos de hello, a continuación, Hola usuario `steve@gmail.com` puede iniciar sesión demasiado`MyDatabase` mediante la opción de autenticación de SSMS hello `Active Directory – Universal with MFA support`. Hello usergroup, de forma predeterminada, tiene solo Hola conectar permiso y los accesos de datos adicionales que necesitarán toobe concedido en hello forma normal. Tenga en cuenta que el usuario `steve@gmail.com` como un usuario invitado debe casilla hello y agregar el nombre de dominio de AD de hello `contosotest.onmicrosoft.com` Hola SSMS **propiedad de conexión** cuadro de diálogo. Hola **identificador de inquilino o el nombre de dominio de AD** opción solo se admite para hello Universal con opciones de conexión de MFA, de lo contrario está atenuada.

## <a name="universal-authentication-limitations-for-sql-database-and-sql-data-warehouse"></a>Limitaciones de Autenticación universal para SQL Database y SQL Data Warehouse
* SSMS y SqlPackage.exe son herramientas solo Hola actualmente habilitados para MFA a través de la autenticación Universal de Active Directory.
* La versión 17.2 de SSMS admite el acceso simultáneo de varios usuarios mediante Autenticación universal con MFA. Versión 17,0 y 17.1, restringido a un inicio de sesión para una instancia de SSMS utilizando autenticación Universal tooa la única cuenta de Azure Active Directory. toolog en otra cuenta de Azure AD, debe utilizar otra instancia de SSMS. (Esta restricción es limitado tooActive autenticación Universal de directorio; puede iniciar sesión en servidores de toodifferent mediante autenticación de contraseña de Active Directory, la autenticación integrada de Active Directory o la autenticación de SQL Server).
* SSMS admite Autenticación universal de Active Directory para la visualización de Explorador de objetos, Editor de consultas y Almacén de consultas.
* La versión 17.2 de SSMS proporciona compatibilidad con el asistente de DacFx para la base de datos de exportación, extracción e implementación. Una vez que un usuario específico se autentica mediante el cuadro de diálogo de autenticación inicial de hello mediante la autenticación de Universal, hello las funciones del Asistente de DacFx Hola mismo modo que lo hace para todos los demás métodos de autenticación.
* Hola Diseñador de tablas de SSMS no admite la autenticación Universal.
* No hay ningún requisito de software adicional para Autenticación universal de Active Directory, excepto el uso de una versión compatible de SSMS.  
* versión de la biblioteca de autenticación de Active Directory (ADAL) de Hello para la autenticación Universal fue la versión de ADAL.dll 3.13.9 disponibles libera más reciente de tooits actualizada. Consulte [Biblioteca de autenticación de Active Directory 3.14.1](http://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/).


## <a name="next-steps"></a>Pasos siguientes

- Para ver los pasos de configuración, consulte [Configure Azure SQL Database multi-factor authentication for SQL Server Management Studio](sql-database-ssms-mfa-authentication-configure.md) (Configuración de la autenticación multifactor de Azure SQL Database para SQL Server Management Studio).
- Conceda otros usuarios tienen acceso a la base de datos de tooyour: [autorización y autenticación de base de datos de SQL: conceder acceso](sql-database-manage-logins.md)  
- Asegúrese de que otros usuarios pueden conectarse a través de firewall de hello: [regla de firewall de configurar un nivel de servidor de base de datos de SQL Azure mediante Hola portal de Azure](sql-database-configure-firewall-settings.md)  
- [Configuración y administración de la autenticación de Azure Active Directory con SQL Database o SQL Data Warehouse](sql-database-aad-authentication-configure.md)  
- [Microsoft SQL Server Data-Tier Application Framework (17.0.0 GA)](https://www.microsoft.com/download/details.aspx?id=55088)  
- [SQLPackage.exe](https://msdn.microsoft.com/library/hh550080.aspx)  
- [Importar un tooa de archivo BACPAC nueva base de datos de SQL Azure](../sql-database/sql-database-import.md)  
- [Exportar un archivo BACPAC de tooa de base de datos de SQL Azure](../sql-database/sql-database-export.md)  
- Interfaz de C# [Interfaz IUniversalAuthProvider](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.iuniversalauthprovider.aspx)  
