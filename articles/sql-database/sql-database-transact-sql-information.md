---
title: "base de datos SQL de Azure de migración de las diferencias de T-SQL aaaResolving | Documentos de Microsoft"
description: Instrucciones de Transact-SQL que no son totalmente compatibles con la Base de datos SQL de Azure
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: c05abd9e-28a7-4c97-9bdf-bc60d08fc92e
ms.service: sql-database
ms.custom: load & move data
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 03/17/2017
ms.author: rickbyh
ms.openlocfilehash: 3852013338bfdc6c7da9d1d879c54781682bc635
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="resolving-transact-sql-differences-during-migration-toosql-database"></a>Resolver diferencias de Transact-SQL durante la migración tooSQL base de datos   
Cuando [migrar la base de datos](sql-database-cloud-migrate.md) de SQL Server tooAzure SQL Server, es posible que descubra que la base de datos requiere algunos reintegración antes de Hola se pueden migrar a SQL Server. Este tema proporciona tooassist de orientación en realizar dicha reestructuración tanto descripción Hola subyacente por qué razones Hola reintegración es necesario. incompatibilidades de toodetect, usar hello [Asistente de migración de datos (DMA)](https://www.microsoft.com/download/details.aspx?id=53595).

## <a name="overview"></a>Información general
La mayoría de las características de Transact-SQL que usan las aplicaciones se admiten en Microsoft SQL Server y Azure SQL Database. Por ejemplo, Hola componentes principales de SQL, como tipos de datos, operadores, cadena, operadores aritméticos, lógicos y funciones de cursor, funcionan exactamente igual en SQL Server y base de datos SQL. Pero hay algunas diferencias de T-SQL en los elementos DDL (lenguaje de definición de datos) y DML (lenguaje de manipulación de datos) que generan instrucciones y consultas de T-SQL que solo se admiten parcialmente (como se describe más adelante en este tema).

Además, existen algunas características y sintaxis que no se admite en absoluto porque base de datos de SQL Azure está diseñado tooisolate características de las dependencias de la base de datos maestra de Hola y sistema operativo de Hola. Por eso, muchas actividades de nivel de servidor no son apropiadas para SQL Database. Las instrucciones y opciones de T-SQL no están disponibles si configuran opciones de nivel de servidor y componentes del sistema operativo, o especifican la configuración del sistema de archivos. Cuando se necesitan estas capacidades, suele estar disponible una alternativa adecuada en alguna otra manera de SQL Database o de otra función o servicio de Azure. 

Por ejemplo, la alta disponibilidad se crea en Azure, para configurar Always On no es necesario (aunque quizás quieran tooconfigure la replicación geográfica activa para una recuperación más rápida en caso de hello de un desastre). Por lo tanto, las instrucciones de T-SQL relacionados con grupos tooavailability no son compatibles con la base de datos SQL, y tampoco se admiten vistas de administración dinámica Hola relacionados tooAlways en.

Para obtener una lista de características de Hola que son compatibles y no compatibles con la base de datos SQL, consulte [comparación de características de base de datos de SQL Azure](sql-database-features.md). lista de Hello en esta página complementa ese tema instrucciones y funciones y se centra en las instrucciones de Transact-SQL.

## <a name="transact-sql-syntax-statements-with-partial-differences"></a>Instrucciones de sintaxis de Transact-SQL con diferencias parciales
instrucciones de DDL (lenguaje de definición de datos) de núcleo de Hello están disponibles, pero algunas instrucciones de DDL tienen selección de ubicación de las extensiones toodisk relacionados y características no admitidas. 

- Las instrucciones CREATE y ALTER DATABASE tienen más de 30 opciones. las instrucciones de Hello incluyen opciones de service broker que se aplican solo tooSQL Server, FILESTREAM y ubicación de los archivos. Esto puede no afectar a si se crean las bases de datos antes de migrar, pero si va a migrar el código de T-SQL que crea las bases de datos se debe comparar [CREATE DATABASE (base de datos de SQL Azure)](https://msdn.microsoft.com/library/dn268335.aspx) con la sintaxis de SQL Server de hello en [crear Base de datos (SQL Server Transact-SQL)](https://msdn.microsoft.com/library/ms176061.aspx) toomake seguro se admiten todas las opciones de Hola que usar. Crear base de datos para la base de datos de SQL Azure también tiene el objetivo de servicio y opciones de escalado flexible que se aplican solo tooSQL base de datos.
- las instrucciones CREATE y ALTER TABLE de Hello tienen opciones FileTable que no se puede usar en la base de datos SQL porque no se admite FILESTREAM.
- Se admiten las instrucciones de inicio de sesión CREATE y ALTER pero base de datos SQL no ofrece todas las opciones de Hola. toomake que fomenta el uso de la base de datos más portable, base de datos SQL incluidos los usuarios de base de datos en lugar de los inicios de sesión siempre que sea posible. Para más información, vea [CREATE/ALTER LOGIN](https://msdn.microsoft.com/library/ms189828.aspx) y [Control y concesión de acceso a bases de datos](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins).

## <a name="transact-sql-syntax-not-supported-in-sql-database"></a>Sintaxis de Transact-SQL no admitida en SQL Database   
Además toohello relacionados de instrucciones SQL tooTransact no admite características que se describen en [comparación de características de base de datos de SQL Azure](sql-database-features.md), Hola siguiendo las instrucciones y los grupos de instrucciones, no se admiten. Por lo tanto, si la base de datos toobe migrado es mediante cualquiera de hello siguientes características, volver a diseñar la tooeliminate de T-SQL estas características de T-SQL y las instrucciones.

- Intercalación de objetos del sistema
- Conexión relacionada: instrucciones de punto de conexión, `ORIGINAL_DB_NAME`. Base de datos SQL no admite la autenticación de Windows, pero admite la autenticación de Azure Active Directory similar de Hola. Algunos tipos de autenticación requieren la versión más reciente de Hola de SSMS. Para obtener más información, consulte [tooSQL de conexión base de datos o SQL datos almacenamiento mediante Azure Active Directory autenticación](sql-database-aad-authentication.md).
- Consultas entre bases de datos con tres o cuatro nombres de partes. (Las consultas entre bases de datos de solo lectura se admiten mediante el uso de [consultas de base de datos elástica](sql-database-elastic-query-overview.md)).
- Encadenamiento de propiedad entre bases de datos, configuración `TRUSTWORTHY`
- `DATABASEPROPERTY` Se usa `DATABASEPROPERTYEX` en su lugar.
- `EXECUTE AS LOGIN` Use "EXECUTE AS USER" en su lugar.
- Se admite el cifrado excepto para la administración extensible de claves.
- Eventos: eventos, notificaciones de eventos, notificaciones de consulta
- Ubicación de los archivos: archivos de base de datos que se administran automáticamente por Microsoft Azure, el tamaño y ubicación de los archivos toodatabase relacionados con la sintaxis.
- Alta disponibilidad: sintaxis relacionada con la disponibilidad de toohigh, que se administra a través de su cuenta de Microsoft Azure. Esto incluye la sintaxis de las copias de seguridad, restauración, Siempre activado, creación de reflejos de las bases de datos, trasvase de registros, modos de recuperación.
- Lector del registro: sintaxis que se basa en el registro del log hello, que no está disponible en la base de datos SQL: la replicación de inserción, la captura de datos modificados. SQL Database puede estar suscrito a un artículo de replicación de inserción.
- Funciones: `fn_get_sql`, `fn_virtualfilestats`, `fn_virtualservernodes`
- Tablas temporales globales
- Hardware: Servidor relacionadas con toohardware valores relacionados con la sintaxis: por ejemplo, memoria, subprocesos de trabajo, la afinidad de CPU, marcas de seguimiento. Usar en su lugar niveles de servicio.
- `HAS_DBACCESS`
- `KILL STATS JOB`
- `OPENQUERY`, `OPENROWSET`, `OPENDATASOURCE` y nombres de cuatro partes
- .NET Framework: integración de CLR con SQL Server
- Búsqueda semántica
- Credenciales de servidor: use [credenciales con ámbito de base de datos](https://msdn.microsoft.com/library/mt270260.aspx) en su lugar.
- Elementos de nivel de servidor: roles de servidor, `IS_SRVROLEMEMBER`, `sys.login_token`. `GRANT`, `REVOKE` y `DENY` de los permisos de nivel de servidor no están disponibles, aunque algunos se sustituyen por permisos en el nivel de base de datos. Algunos DMV útiles de nivel de servidor cuentan con DMV equivalentes de nivel de base de datos.
- `SET REMOTE_PROC_TRANSACTIONS`
- `SHUTDOWN`
- `sp_addmessage`
- Opciones de `sp_configure` y `RECONFIGURE`. Algunas opciones están disponibles mediante [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx).
- `sp_helpuser`
- `sp_migrate_user_to_contained`
- Agente SQL Server: Sintaxis que se basa en la base de datos MSDB de agente SQL Server o hello de hello: alertas, operadores, servidores de administración central. Use el scripting como Azure PowerShell en su lugar.
- Auditoría de SQL Server: usar auditoría de Base de datos SQL en su lugar.
- Seguimiento de SQL Server
- Marcas de seguimiento: algunos marca de seguimiento elementos han sido movido toocompatibility modos.
- Depuración de Transact-SQL
- Desencadenadores: desencadenadores LOGON o con ámbito de servidor
- `USE`instrucción: toochange Hola base de datos contexto tooa base de datos diferente, debe realizar una nueva conexión toohello nueva base de datos.

## <a name="full-transact-sql-reference"></a>Referencia completa de Transact-SQL
Para obtener más información sobre la gramática de Transact-SQL, su uso y ejemplos, consulte [Referencia de Transact-SQL (motor de base de datos)](https://msdn.microsoft.com/library/bb510741.aspx) en Libros en pantalla de SQL Server. 

### <a name="about-hello-applies-to-tags"></a>Acerca de las etiquetas "Se aplica a" hello
Hola referencia de Transact-SQL incluye temas relacionados tooSQL Server versiones 2008 toohello presente. A continuación del título del tema Hola hay una barra de iconos, plataformas de SQL Server cuatro de anuncio Hola y aplicabilidad e indica. Por ejemplo, los grupos de disponibilidad se introdujeron en SQL Server 2012. El [crear grupo de disponibilidad](https://msdn.microsoft.com/library/ff878399.aspx) tema indica que la declaración de Hola se aplica a **(a partir de 2012) de SQL Server**. instrucción de Hello no aplica tooSQL Server 2008, SQL Server 2008 R2, base de datos de SQL Azure, almacenamiento de datos de SQL Azure o almacenamiento de datos paralelos.

En algunos casos, Hola general de un tema puede utilizarse en un producto, pero hay pequeñas diferencias entre los productos. se indican las diferencias de Hello en puntos medios en el tema de hello según corresponda. En algunos casos, Hola general de un tema puede utilizarse en un producto, pero hay pequeñas diferencias entre los productos. se indican las diferencias de Hello en puntos medios en el tema de hello según corresponda. Por ejemplo tema CREATE TRIGGER de hello está disponible en la base de datos SQL. Pero hello **ALL SERVER** opción de desencadenadores de nivel de servidor, indica que no se puede utilizar desencadenadores del servidor de base de datos de SQL. Use desencadenadores de nivel de base de datos en su lugar.

## <a name="next-steps"></a>Pasos siguientes

Para obtener una lista de características de Hola que son compatibles y no compatibles con la base de datos SQL, consulte [comparación de características de base de datos de SQL Azure](sql-database-features.md). lista de Hello en esta página complementa ese tema instrucciones y funciones y se centra en las instrucciones de Transact-SQL.

