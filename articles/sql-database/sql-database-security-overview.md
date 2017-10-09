---
title: "información general de seguridad de base de datos de SQL aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de la seguridad de base de datos de SQL Azure y SQL Server, incluidas las diferencias de hello entre la nube de Hola y SQL Server local cuando se trata de tooauthentication, autorización, seguridad de conexión, cifrado y cumplimiento de normas."
services: sql-database
documentationcenter: 
author: tmullaney
manager: jhubbard
editor: 
ms.assetid: a012bb85-7fb4-4fde-a2fc-cf426c0a56bb
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 07/05/2017
ms.author: thmullan;jackr
ms.openlocfilehash: 7b0b0d1b59ec4018d9fb668bc8b6b56c9907e982
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="securing-your-sql-database"></a>Protección de bases de datos SQL

Este artículo le guía a través de los conceptos básicos de Hola de protección de nivel de datos de Hola de una aplicación con la base de datos de SQL Azure. En concreto, este artículo le ayudará a empezar a trabajar con los recursos necesarios para proteger los datos, controlar el acceso y realizar una supervisión proactiva. 

Para obtener información general completa de características de seguridad disponibles en todos los tipos de SQL, vea hello [centro de seguridad para el motor de base de datos de SQL Server y base de datos de SQL Azure](https://msdn.microsoft.com/library/bb510589). Información adicional también está disponible en hello [seguridad y la base de datos de SQL Azure documentación técnica](https://download.microsoft.com/download/A/C/3/AC305059-2B3F-4B08-9952-34CDCA8115A9/Security_and_Azure_SQL_Database_White_paper.pdf) (PDF).

## <a name="protect-data"></a>Protección de datos
SQL Database protege los datos mediante el cifrado de los datos en movimiento a través de [Seguridad de la capa de transporte](https://support.microsoft.com/kb/3135244), de los datos en reposo a través de [Cifrado de datos transparente](http://go.microsoft.com/fwlink/?LinkId=526242) y de los datos de uso a través de [Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx). 

> [!IMPORTANT]
>Todas las conexiones tooAzure base de datos SQL requiere el cifrado (SSL/TLS) en todo momento mientras los datos están "en tránsito" tooand de base de datos de Hola. En la cadena de conexión de la aplicación, debe especificar conexión de Hola de parámetros tooencrypt y *no* tootrust Hola certificado de servidor (Esto se hace para que, si copia la cadena de conexión de Hola Portal clásico de Azure) en caso contrario, conexión hello no comprobará la identidad Hola Hola al servidor y será susceptibles de sufrir ataques de demasiado "man-in-the-middle". Para el controlador ADO.NET de hello, por ejemplo, estos parámetros de cadena de conexión están **Encrypt = True** y **TrustServerCertificate = False**. 

Para otro tooencrypt formas los datos, tenga en cuenta:

* [Cifrado de nivel de celda](https://msdn.microsoft.com/library/ms179331.aspx) tooencrypt columnas específicas o incluso las celdas de datos con distintas claves de cifrado.
* Si necesita un módulo de seguridad de hardware o la administración central de la jerarquía de claves de cifrado, considere la posibilidad de usar [Azure Key Vault con SQL Server en una máquina virtual de Azure](http://blogs.technet.com/b/kv/archive/2015/01/12/using-the-key-vault-for-sql-server-encryption.aspx).

## <a name="control-access"></a>Control de acceso
Base de datos SQL protege los datos mediante la limitación de base de datos de access tooyour mediante las reglas de firewall que requieren los usuarios tooprove su identidad y autorización toodata a través de pertenencia basada en roles y permisos, así como a través de mecanismos de autenticación seguridad de nivel de fila y enmascaramiento dinámico de datos. Para obtener una explicación del uso de Hola de características de control de acceso en la base de datos SQL, consulte [controlar el acceso](sql-database-control-access.md).

> [!IMPORTANT]
> La administración de bases de datos y servidores lógicos en Azure se controlan mediante las asignaciones de roles de su cuenta de usuario del portal. Para obtener más información sobre este tema, consulte [Control de acceso basado en rol en el Portal de Azure](../active-directory/role-based-access-control-what-is.md).
>

### <a name="firewall-and-firewall-rules"></a>Firewall y reglas de firewall
toohelp proteger los datos, los servidores de seguridad evita que todos los servidores de base de datos de access tooyour hasta que especifique qué equipos tienen permiso [las reglas de firewall](sql-database-firewall-configure.md). firewall de Hello otorga toodatabases de acceso basado en hello procedentes de la dirección IP de cada solicitud.

### <a name="authentication"></a>Autenticación
Autenticación de base de datos SQL refiere toohow demostrar su identidad cuando se conecta la base de datos de toohello. SQL Database admite dos tipos de autenticación:

* **Autenticación de SQL**, que usa un nombre de usuario y una contraseña. Cuando crea el servidor lógico de hello para la base de datos, especificar un inicio de sesión de "administrador del servidor" con un nombre de usuario y una contraseña. Con estas credenciales, puede autenticar tooany base de datos en ese servidor como propietario de la base de datos de Hola o "dbo". 
* **Autenticación de Azure Active Directory**, que usa las identidades administradas por Azure Active Directory y es compatible con dominios administrados e integrados. Use la autenticación de Active Directory (seguridad integrada) [siempre que sea posible](https://msdn.microsoft.com/library/ms144284.aspx). Si desea toouse autenticación de Azure Active Directory, debe crear otro administrador de servidor llamado hello "Azure AD admin", que se permite grupos y usuarios de Azure AD tooadminister. Este administrador también puede realizar todas las operaciones de un administrador de servidor normal. Vea [conectar tooSQL base de datos mediante Active Directory autenticación de Azure](sql-database-aad-authentication.md) para ver un tutorial sobre cómo toocreate una tooenable de administración de Azure AD autenticación de Azure Active Directory.

### <a name="authorization"></a>Autorización
La autorización refiere toowhat puede hacer un usuario dentro de una base de datos de SQL Azure y es controlada por la pertenencia a roles de base de datos de su cuenta de usuario y de nivel de objeto permisos. Como práctica recomendada, debe conceder Hola usuarios privilegios mínimos necesarios. cuenta de administrador de servidor de saludo con que se está conectando es un miembro de db_owner, que tiene autoridad toodo cualquier elemento dentro de la base de datos de Hola. Guarde esta cuenta para implementar las actualizaciones de los esquemas y otras operaciones de administración. Usar cuenta de "ApplicationUser" hello con más limitada tooconnect de permisos de la base de datos de aplicación toohello con hello privilegios mínimos necesarios para la aplicación.

### <a name="row-level-security"></a>Seguridad de nivel de fila
Seguridad de nivel de fila permite a los clientes toocontrol acceso toorows en una tabla de base de datos basada en características de Hola de usuario de Hola que se ejecuta una consulta (por ejemplo, grupo pertenencia o contexto de ejecución). Para más información, consulte [Seguridad de nivel de fila](https://msdn.microsoft.com/library/dn765131).

### <a name="data-masking"></a>Enmascaramiento de datos 
Enmascaramiento de datos dinámicos de la base de datos SQL limita la exposición de información confidencial ocultándola a los usuarios privilegios toonon. Automáticamente enmascaramiento dinámico de datos detecta datos potencialmente confidenciales en la base de datos de SQL Azure y proporciona recomendaciones útiles toomask estos campos, con un impacto mínimo en el nivel de aplicación Hola. Funciona ocultándola confidencial Hola Hola conjunto de resultados de una consulta de campos de la base de datos designada, mientras que no cambian datos hello en la base de datos de Hola. Para obtener más información, consulte [empezar a trabajar con enmascaramiento de datos dinámicos de la base de datos SQL](sql-database-dynamic-data-masking-get-started.md) puede ser usado toolimit la exposición de información confidencial.

## <a name="proactive-monitoring"></a>Supervisión proactiva
SQL Database protege los datos proporcionando funcionalidades de auditoría y detección de amenazas. 

### <a name="auditing"></a>Auditoría
Auditoría de base de datos de SQL Server realiza un seguimiento de las actividades de la base de datos y le ayuda a toomaintain el cumplimiento de normas, al registrar el registro de auditoría de base de datos eventos tooan en su cuenta de almacenamiento de Azure. Auditoría permite toounderstand actividades de base de datos en curso, así como analizar e investigar posibles amenazas de actividad histórica tooidentify o supuestas infracciones de seguridad y controlar el abuso. Para más información, consulte [Introducción a SQL Database Auditing](sql-database-auditing.md).  

### <a name="threat-detection"></a>Detección de amenazas
La detección de amenazas complementa la auditoría, proporcionando una capa adicional de inteligencia de seguridad integrada en el servicio de base de datos de SQL Azure Hola que detecta intentos inusuales y potencialmente dañino tooaccess o vulnerabilidad bases de datos. Recibirá alertas de actividades sospechosas, vulnerabilidades potenciales y ataques pon inyección de código SQL, así como patrones anómalos de acceso a bases de datos. Se pueden ver las alertas de detección de amenazas en [Azure Security Center](https://azure.microsoft.com/services/security-center/) y proporcionar detalles de actividad sospechosa y recomendarán acción sobre cómo tooinvestigate y mitigar la amenaza de Hola. Detección de amenazas cuesta 15 USD/servidor/mes. Será gratuito para hello primeros 60 días. Para más información, consulte [Introducción a Detección de amenazas de Base de datos SQL](sql-database-threat-detection.md).
 
### <a name="data-masking"></a>Enmascaramiento de datos 
Enmascaramiento de datos dinámicos de la base de datos SQL limita la exposición de información confidencial ocultándola a los usuarios privilegios toonon. Automáticamente enmascaramiento dinámico de datos detecta datos potencialmente confidenciales en la base de datos de SQL Azure y proporciona recomendaciones útiles toomask estos campos, con un impacto mínimo en el nivel de aplicación Hola. Funciona ocultándola confidencial Hola Hola conjunto de resultados de una consulta de campos de la base de datos designada, mientras que no cambian datos hello en la base de datos de Hola. Para más información, vea la introducción al [Enmascaramiento dinámico de datos de SQL Database](sql-database-dynamic-data-masking-get-started.md).
 
## <a name="compliance"></a>Cumplimiento normativo
Además toohello encima de características y funcionalidad que puede ayudar a la aplicación a cumplir distintos requisitos de seguridad, base de datos de SQL Azure también participa en auditorías periódicas y ha sido certificado con un número de estándares de cumplimiento. Para obtener más información, vea hello [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/), donde puede encontrar la lista más reciente de Hola de [certificaciones de cumplimiento de la base de datos SQL](https://azure.microsoft.com/support/trust-center/services/).

## <a name="next-steps"></a>Pasos siguientes

- Para obtener una explicación del uso de Hola de características de control de acceso en la base de datos SQL, consulte [controlar el acceso](sql-database-control-access.md).
- Para más información sobre la auditoría de bases de datos, consulte [SQL Database auditing](sql-database-auditing.md) (Auditoría de SQL Database).
- Para más información sobre la detección de amenaza, consulte [SQL Database threat detection](sql-database-threat-detection.md) (Detección de amenazas de SQL Database).
