---
title: aaaAuthentication tooAzure almacenamiento de datos SQL | Documentos de Microsoft
description: Azure Active Directory (AAD) y SQL Server authentication tooAzure almacenamiento de datos SQL.
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
tags: 
ms.assetid: fefaaa75-2d0c-4e5d-aadb-410342d1ad73
ms.service: sql-data-warehouse
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.custom: security
ms.date: 03/21/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 66673ce1d4761243755254c8f64de1078a0ea82e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-tooazure-sql-data-warehouse"></a>Autenticación tooAzure almacenamiento de datos SQL
> [!div class="op_single_selector"]
> * [Información general sobre seguridad](sql-data-warehouse-overview-manage-security.md)
> * [Autenticación](sql-data-warehouse-authentication.md)
> * [Cifrado (Portal)](sql-data-warehouse-encryption-tde.md)
> * [Cifrado (T-SQL)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

tooconnect tooSQL almacenamiento de datos, debe pasar las credenciales de seguridad para la autenticación. Después de establecer una conexión, determinados valores de conexión se configuran como parte del establecimiento de la sesión de la consulta.  

Para obtener más información sobre la seguridad y cómo tooenable almacenamiento de datos de las conexiones tooyour, consulte [proteger una base de datos en el almacén de datos de SQL][Secure a database in SQL Data Warehouse].

## <a name="sql-authentication"></a>Autenticación de SQL
tooconnect tooSQL almacenamiento de datos, debe proporcionar Hola siguiente información:

* Nombre de servidor completo
* Especificar la autenticación de SQL
* Nombre de usuario
* Password
* Base de datos predeterminada (opcional)

De forma predeterminada la conexión conecta toohello *maestro* base de datos y no la base de datos de usuario. base de datos de usuario de tooyour tooconnect, puede elegir toodo una de estas dos cosas:

* Especificar base de datos de hello predeterminada al registrar el servidor con el Explorador de objetos de SQL Server en SSDT, SSMS, o en la cadena de conexión de la aplicación hello. Por ejemplo, incluir parámetro InitialCatalog de hello para una conexión ODBC.
* Resalte la base de datos de usuario de hello antes de crear una sesión en SSDT.

> [!NOTE]
> Hola instrucción Transact-SQL **uso MyDatabase;** no se admite para cambiar base de datos de Hola para una conexión. Para obtener instrucciones conectar tooSQL almacenamiento de datos con SSDT, consulte toohello [consulta con Visual Studio] [ Query with Visual Studio] artículo.
> 
> 

## <a name="azure-active-directory-aad-authentication"></a>Autenticación de Azure Active Directory (AAD)
[Azure Active Directory] [ What is Azure Active Directory] autenticación es un mecanismo de conexión tooMicrosoft almacenamiento de datos de SQL Azure mediante el uso de identidades en Azure Active Directory (Azure AD). Con la autenticación de Azure Active Directory, puede administrar de forma centralizada las identidades de Hola de usuarios de base de datos y otros servicios de Microsoft en una ubicación central. Administración del identificador central proporciona un único lugar a los usuarios de almacenamiento de datos SQL de toomanage y simplifica la administración de permisos. 

### <a name="benefits"></a>Ventajas
Entre las ventajas de Azure Active Directory, se incluyen:

* Proporciona una autenticación del servidor tooSQL alternativo.
* Ayuda a detener la proliferación de Hola de identidades de usuario entre los servidores de base de datos.
* Permite la rotación de contraseñas en un solo lugar
* Permite administrar los permisos de la base de datos con grupos externos (AAD).
* Elimina el almacenamiento de contraseñas mediante la habilitación de la autenticación integrada de Windows y otras formas de autenticación compatibles con Azure Active Directory.
* Usa contenido tooauthenticate identidades de los usuarios de base de datos en el nivel de base de datos de Hola.
* Admite la autenticación basada en autorización token de aplicaciones que se conectan tooSQL almacenamiento de datos.
* Admite Multi-Factor Authentication mediante autenticación universal de Active Directory para SQL Server Management Studio. Para una descripción de Multi-Factor Authentication, consulte [Compatibilidad de SSMS con Azure AD MFA con Base de datos SQL y Almacenamiento de datos SQL](../sql-database/sql-database-ssms-mfa-authentication.md).

> [!NOTE]
> Azure Active Directory todavía es relativamente nuevo y tiene algunas limitaciones. tooensure que Azure Active Directory es una buena elección para su entorno, consulte [características de Azure AD y limitaciones][Azure AD features and limitations], concretamente Hola consideraciones adicionales.
> 
> 

### <a name="configuration-steps"></a>Pasos de configuración
Siga estos autenticación de Azure Active Directory tooconfigure pasos.

1. Crear y rellenar un Azure Active Directory.
2. Opcional: Asociar o cambiar Hola active directory que está asociada actualmente con la suscripción de Azure
3. Crear un administrador de Azure Active Directory para Almacenamiento de datos SQL de Azure.
4. Configurar los equipos cliente.
5. Crear usuarios de base de datos independiente en la base de datos asignado tooAzure identidades de AD
6. Conectar almacenamiento de datos de tooyour mediante identidades de Azure AD

Actualmente los usuarios de Azure Active Directory no se muestran en el Explorador de objetos de SSDT. Como alternativa, ver los usuarios de hello en [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).

### <a name="find-hello-details"></a>Conocer los detalles de Hola
* autenticación de Azure Active Directory de tooconfigure y el uso de los pasos de Hello son casi idénticos para la base de datos de SQL Azure y almacenamiento de datos de SQL Azure. Siga Hola detallan los pasos en el tema de hello [tooSQL de conexión base de datos o SQL datos almacenamiento mediante Azure Active Directory autenticación](../sql-database/sql-database-aad-authentication.md).
* Crear roles de base de datos personalizada y agregue usuarios toohello funciones. A continuación, conceder permisos granulares toohello roles. Para obtener más información, consulte [Introducción a los permisos de los motores de bases de datos](https://msdn.microsoft.com/library/mt667986.aspx).

## <a name="next-steps"></a>Pasos siguientes
toostart consultar el almacenamiento de datos con Visual Studio y otras aplicaciones, consulte [consulta con Visual Studio][Query with Visual Studio].

<!-- Article references -->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[What is Azure Active Directory]: ../active-directory/active-directory-whatis.md
[Azure AD features and limitations]: ../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations
