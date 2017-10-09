---
title: aaaSecuring bases de datos de PaaS de Azure | Documentos de Microsoft
description: " Obtenga información sobre los procedimientos recomendados de seguridad de Azure SQL Database y SQL Data Warehouse para proteger las aplicaciones web y móviles PaaS. "
services: security
documentationcenter: na
author: techlake
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: terrylan
ms.openlocfilehash: a7f9a2846b59dcb05e82f2ad88b41c5213295603
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="securing-paas-databases-in-azure"></a>Protección de bases de datos de PaaS en Azure

En este artículo se presenta una colección de procedimientos recomendados de seguridad de [Azure SQL Database](https://azure.microsoft.com/services/sql-database/) y [SQL Data Warehouse](https://azure.microsoft.com/services/sql-data-warehouse/) para proteger las aplicaciones web y móviles PaaS. Estas prácticas recomendadas se derivan de nuestra experiencia con Azure y experiencias de Hola de clientes como usted mismo.

## <a name="azure-sql-database-and-sql-data-warehouse"></a>Azure SQL Database y SQL Data Warehouse
[Azure SQL Database](../sql-database/sql-database-technical-overview.md) y [SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) proporcionan un servicio de base de datos relacional para aplicaciones basadas en Internet. Se van a considerar los servicios que ayudan a proteger las aplicaciones y los datos al utilizar Azure SQL Database y SQL Data Warehouse en una implementación de PaaS:

- Autenticación de Azure Active Directory (en lugar de la autenticación de SQL Server)
- Firewall de Azure SQL
- Cifrado de datos transparente (TDE) 

## <a name="best-practices"></a>Prácticas recomendadas

### <a name="use-a-centralized-identity-repository-for-authentication-and-authorization"></a>Uso de un repositorio centralizado de identidades para autenticación y autorización

Bases de datos SQL Azure pueden ser toouse configurado uno de dos tipos de autenticación:

- **Autenticación de SQL** usa un nombre de usuario y una contraseña. Cuando crea el servidor lógico de hello para la base de datos, especificar un inicio de sesión de "administrador del servidor" con un nombre de usuario y una contraseña. Estas credenciales se puede autenticar tooany base de datos en ese servidor como propietario de la base de datos de Hola.

- **Autenticación de Azure Active Directory** usa las identidades administradas por Azure Active Directory y es compatible con dominios administrados e integrados. toouse autenticación de Azure Active Directory, debe crear otro administrador de servidor llamado hello "Azure AD admin", que se permite grupos y usuarios de Azure AD tooadminister. Este administrador también puede realizar todas las operaciones de un administrador de servidor normal.

[Autenticación de Azure Active Directory](../active-directory/develop/active-directory-authentication-scenarios.md) es un mecanismo de conexión tooAzure base de datos SQL y almacenamiento de datos de SQL mediante el uso de identidades en Azure Active Directory (AD). Azure AD proporciona una autenticación de servidor alternativo tooSQL por lo que puede detener la proliferación de Hola de identidades de usuario a través de servidores de base de datos. Habilita la autenticación AD Azure toocentrally administrar identidades de Hola de usuarios de base de datos y otros servicios de Microsoft en una ubicación central. Administración del identificador central proporciona un único lugar a los usuarios de base de datos de toomanage y simplifica la administración de permisos.  

Entre las ventajas de utilizar la autenticación de Azure AD en lugar de la autenticación de SQL se incluyen:

- Permite la rotación de contraseñas en un solo lugar.
- Administra los permisos de la base de datos con grupos externos de Azure AD.
- Elimina el almacenamiento de contraseñas mediante la habilitación de la autenticación integrada de Windows y otras formas de autenticación compatibles con Azure AD.
- Usa contenido tooauthenticate identidades de los usuarios de base de datos en el nivel de base de datos de Hola.
- Admite la autenticación basada en autorización token de aplicaciones que se conectan tooSQL base de datos.
- Es compatible con ADFS (federación de dominios) o la autenticación nativa de usuario y contraseña para una instancia de Azure AD local sin sincronización de dominios.
- Admite conexiones de SQL Server Management Studio que usan la autenticación universal de Active Directory, lo cual incluye [Multi-Factor Authentication (MFA)](../multi-factor-authentication/multi-factor-authentication.md). MFA incluye una sólida autenticación con una gama de sencillas opciones de comprobación: llamada de teléfono, mensaje de texto, tarjetas inteligentes con PIN o notificación de aplicación móvil. Para obtener más información, consulte [Compatibilidad de SSMS con Azure AD MFA con Base de datos SQL y Almacenamiento de datos SQL](../sql-database/sql-database-ssms-mfa-authentication.md).

toolearn más información acerca de la autenticación de Azure AD, consulte:

- [Conectar tooSQL base de datos o SQL datos almacenamiento mediante Active Directory autenticación de Azure](../sql-database/sql-database-aad-authentication.md)
- [Autenticación tooAzure almacenamiento de datos SQL](../sql-data-warehouse/sql-data-warehouse-authentication.md)
- [Token-based authentication support for Azure SQL DB using Azure AD authentication](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth/) (Compatibilidad de la autenticación basada en tokens para Azure SQL DB mediante la autenticación de Azure AD)

> [!NOTE]
> tooensure que Azure Active Directory es una buena elección para su entorno, consulte [características de Azure AD y limitaciones](../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations), concretamente Hola consideraciones adicionales.
>
>

### <a name="restrict-access-based-on-ip-address"></a>Restricción de acceso según la dirección IP
Puede crear reglas de firewall que especifiquen intervalos de direcciones IP aceptables. Estas reglas se pueden inscribir en servidor hello y niveles de base de datos. Se recomienda usar las reglas de firewall de nivel de base de datos siempre que sea posible tooenhance seguridad y toomake la base de datos más portátil. Las reglas de firewall de nivel de servidor son útiles para los administradores y si tiene muchas bases de datos que han Hola mismos requisitos de acceso, pero no desea tiempo toospend configurar individualmente cada base de datos.

Las restricciones de direcciones IP de origen predeterminadas de SQL Database permiten acceder desde cualquier dirección de Azure (incluidos otras suscripciones y otros inquilinos). Puede restringir este tooonly permitir que la instancia de Hola de tooaccess de direcciones IP. A pesar de las restricciones de direcciones IP y del firewall de SQL, también se necesita una autenticación sólida. Ver recomendaciones de hello realizadas anteriormente en este artículo.

toolearn más información sobre Firewall de SQL Azure y las restricciones de IP, vea:

- [Control de acceso a Azure SQL Database](../sql-database/sql-database-control-access.md)
- [Introducción a la configuración de reglas de firewall de Azure SQL Database](../sql-database/sql-database-firewall-configure.md)
- [Configurar una regla de firewall de nivel de servidor de base de datos de SQL Azure mediante Hola portal de Azure](../sql-database/sql-database-configure-firewall-settings.md)

### <a name="encryption-of-data-at-rest"></a>Cifrado de datos en reposo
[Cifrado de datos transparente (TDE)](https://msdn.microsoft.com/library/azure/bb934049) está habilitado de forma predeterminada. TDE cifra de forma transparente los archivos de datos y de registro de SQL Server, Azure SQL Database y Azure SQL Data Warehouse. TDE protege contra un posible peligro de archivos de toohello de acceso directo o su copia de seguridad. Esto le permite tooencrypt datos en reposo sin cambiar las aplicaciones existentes. TDE siempre debería permanecer habilitado; Sin embargo, esto no detendrá un atacante que utiliza la ruta de acceso normal de Hola. TDE proporciona Hola capacidad toocomply con muchas leyes, normativas y directrices establecidas en diversos sectores.

Azure SQL administra los problemas relacionados con las claves para TDE. Como con TDE, de manera local debe tener especial cuidado tooensure la capacidad de recuperación y, al mover bases de datos. En escenarios más complejos, las claves de hello posible explícitamente administrar en el almacén de claves de Azure mediante la administración extensible de claves (vea [habilitar TDE en SQL Server usando EKM](/security/encryption/enable-tde-on-sql-server-using-ekm)). Esto también permite la funcionalidad Bring Your Own Key (BYOK), que incorpora Azure Key Vault.

Azure SQL ofrece cifrado de columnas mediante [Always Encrypted](/sql/relational-databases/security/encryption/always-encrypted-database-engine). Esto permite el acceso de sólo las aplicaciones autorizadas toosensitive columnas. Mediante este tipo de cifrado limita las consultas SQL para los valores de las columnas cifradas basado en tooequality.

También debe usarse el cifrado a nivel de aplicación para datos selectivos. A veces se pueden mitigar preocupaciones soberanía de datos mediante el cifrado de datos con una clave que se mantiene en país o región correcto Hola. Esto impide que la transferencia de datos incluso accidental provocando un problema, ya que es hello toodecrypt imposible datos sin clave hello, suponiendo un algoritmo seguro se usan (por ejemplo, AES 256).

Puede usar la base de datos de precauciones adicionales toohelp Hola segura, como diseñar un sistema seguro, cifrar los activos confidenciales e instalar un firewall alrededor de los servidores de base de datos de Hola.

## <a name="next-steps"></a>Pasos siguientes
En este artículo se introdujo colección del tooa, de base de datos SQL y procedimientos recomendados de seguridad de almacenamiento de datos de SQL para proteger su PaaS aplicaciones web y móviles. toolearn más acerca de cómo proteger las implementaciones de PaaS, vea:

- [Protección de implementaciones de PaaS](security-paas-deployments.md)
- [Protección de aplicaciones web y móviles PaaS con Azure App Services](security-paas-applications-using-app-services.md)
