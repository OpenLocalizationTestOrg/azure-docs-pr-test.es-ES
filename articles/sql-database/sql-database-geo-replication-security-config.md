---
title: "seguridad de base de datos de SQL Azure para la recuperación ante desastres aaaConfigure | Documentos de Microsoft"
description: "En este tema se explica las consideraciones de seguridad para configurar y administrar la seguridad después de una restauración de base de datos o un servidor secundario de tooa de conmutación por error en caso de hello de una interrupción del centro de datos u otros desastres"
services: sql-database
documentationcenter: na
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: c7c898c9-69d4-4e16-8b7e-720bbb3353dd
ms.service: sql-database
ms.custom: business continuity
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 10/13/2016
ms.author: sashan
ms.openlocfilehash: c3172568e1b8ad2a53958200aa6cf19b4a9434ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-manage-azure-sql-database-security-for-geo-restore-or-failover"></a>Configuración y administración de la seguridad de Azure SQL Database para la restauración geográfica o la conmutación por error 

> [!NOTE]
> La [replicación geográfica activa](sql-database-geo-replication-overview.md) está ahora disponible para todas las bases de datos en todos los niveles de servicio.
>  

## <a name="overview-of-authentication-requirements-for-disaster-recovery"></a>Información general sobre los requisitos de autenticación para la recuperación ante desastres
Este tema describe Hola authentication requisitos tooconfigure y control [replicación geográfica activa](sql-database-geo-replication-overview.md) Hola pasos tooset requiere la base de datos de usuario acceso toohello secundaria. También se describe cómo habilitar la base de datos de access toohello recuperado después de usar [georestauración](sql-database-recovery-using-backups.md#geo-restore). Para más información sobre opciones de recuperación, consulte [Información general sobre la continuidad empresarial](sql-database-business-continuity.md).

## <a name="disaster-recovery-with-contained-users"></a>Recuperación ante desastres con usuarios contenidos
A diferencia de usuarios tradicionales, que debe asignarse toologins en la base de datos maestra de hello, un usuario contenido se administra completamente Hola propia base de datos. lo que ofrece dos ventajas. En el escenario de recuperación ante desastres de hello, los usuarios de hello pueden seguir tooconnect toohello nueva base de datos principal o base de datos de hello recuperado utilizando la restauración geográfica sin ninguna configuración adicional, porque los usuarios de Hola encarga de base de datos de Hola. También existen ventajas potenciales de escalabilidad y rendimiento con esta configuración desde la perspectiva del inicio de sesión. Para obtener más información, vea [Usuarios de base de datos independiente - Conversión de la base de datos en portátil](https://msdn.microsoft.com/library/ff929188.aspx). 

ventajas y desventajas de Hello principal son que es más difícil administrar el proceso de recuperación ante desastres de Hola a escala. Si tiene varias bases de datos ese Hola uso mismo inicio de sesión, mantenimiento de las credenciales de hello con contenidos a los usuarios en varias bases de datos pueden invalidar ventajas de Hola de usuarios contenidos. Por ejemplo, directiva de rotación de hello contraseña requiere que se realizan cambios coherente en varias bases de datos en lugar de cambiar la contraseña de inicio de sesión de Hola Hola una vez en la base de datos maestra Hola. Por este motivo, si tiene varias bases de datos que use Hola mismo nombre de usuario y la contraseña, no se recomienda utilizar usuarios contenidos. 

## <a name="how-tooconfigure-logins-and-users"></a>¿Cómo tooconfigure inicios de sesión y usuarios
Si usas los inicios de sesión y usuarios (en lugar de usuarios contenidos), debe seguir tooinsure pasos adicionales que Hola mismos inicios de sesión existen en la base de datos maestra de Hola. Hello siguientes secciones presentan consideraciones implicados y adicional de pasos de Hola.

### <a name="set-up-user-access-tooa-secondary-or-recovered-database"></a>Establecer usuario acceso tooa secundaria o recuperada base de datos
Para hello toobe de base de datos secundaria puede usar como una base de datos secundaria de solo lectura y tooensure el acceso adecuado toohello nuevo principal Hola o base de datos de base de datos recuperar utilizando la restauración geográfica, Hola maestra base de datos del servidor de destino de hello debe tener Hola configuración de seguridad apropiada en su lugar antes de la recuperación de Hola.

permisos específicos de Hola para cada paso se describen más adelante en este tema.

Preparar tooa de acceso de usuario debe realizarse la replicación geográfica secundaria como parte de la configuración de replicación geográfica. Preparación de acceso de usuario restaurado geográfica de toohello las bases de datos debe realizarse en cualquier momento al servidor original de hello está en línea (por ejemplo, como parte de obtención de detalles de recuperación ante desastres de hello).

> [!NOTE]
> Si se produce un error sobre o la restauración geográfica tooa al servidor no tiene inicios de sesión configuradas correctamente, tooit de acceso será limitado toohello cuenta de administrador de servidor.
> 
> 

Configurar inicios de sesión en el servidor de destino de hello implica tres pasos que se describen a continuación:

#### <a name="1-determine-logins-with-access-toohello-primary-database"></a>1. Determinar inicios de sesión con la base de datos de access toohello principal:
Hola primer paso del proceso de hello es toodetermine qué inicios de sesión se deben duplicar en el servidor de destino de Hola. Esto se logra con un par de instrucciones SELECT, una en hello lógico base de datos maestra en el servidor de origen de Hola y de hello principal propia base de datos.

Hola solo el administrador del servidor o un miembro de hello **LoginManager** rol de servidor puede determinar los inicios de sesión de hello en el servidor de origen de hello con hello después de la instrucción SELECT. 

    SELECT [name], [sid] 
    FROM [sys].[sql_logins] 
    WHERE [type_desc] = 'SQL_Login'

Sólo un miembro del rol de base de datos db_owner hello, un usuario de dbo de Hola o administrador del servidor, puede determinar todas Hola entidades de usuario de base de datos en la base de datos principal de Hola de.

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

#### <a name="2-find-hello-sid-for-hello-logins-identified-in-step-1"></a>2. Encontrar Hola SID para los inicios de sesión de hello identificados en el paso 1:
Comparando la salida de hello de consultas de hello de la sección anterior de Hola y Hola coincidente SID, puede asignar el usuario de toodatabase de inicio de sesión de servidor de Hola. Inicios de sesión que tienen un usuario de base de datos con un SID coincidente tienen base de datos de usuario acceso toothat como ese usuario de base de datos principal. 

Hello consulta siguiente puede ser usado toosee todas las entidades de seguridad del usuario de Hola y sus SID en una base de datos. Sólo un miembro de Hola db_owner, base de datos servidor o el rol de administrador puede ejecutar esta consulta.

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

> [!NOTE]
> Hola **INFORMATION_SCHEMA** y **sys** los usuarios tienen *NULL* hello y SID **invitado** SID es **0 x 00**. Hola **dbo** SID puede empezar por *0 x 01060000000001648000000000048454*, si es de creador de base de datos de Hola Hola administrador del servidor en lugar de un miembro de **DbManager**.
> 
> 

#### <a name="3-create-hello-logins-on-hello-target-server"></a>3. Crear inicios de sesión de hello en el servidor de destino de hello:
Hello último paso es el servidor de destino de toogo toohello, o los servidores y generar los inicios de sesión de hello con hello adecuados SID. sintaxis básica de Hello es como sigue.

    CREATE LOGIN [<login name>]
    WITH PASSWORD = <login password>,
    SID = <desired login SID>

> [!NOTE]
> Si desea toogrant usuario acceso toohello base de datos secundaria, pero no toohello principal, puede hacerlo alterando el inicio de sesión de usuario de hello en el servidor principal de hello mediante el uso de hello según la sintaxis.
> 
> ALTER LOGIN <login name> DISABLE
> 
> DISABLE no cambia la contraseña de hello, por lo que siempre puede habilitar si es necesario.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
* Para obtener más información sobre cómo administrar el acceso a la base de datos y los inicios de sesión, consulte [Seguridad de la Base de datos SQL: administrar la seguridad del inicio de sesión y el acceso a la base de datos](sql-database-manage-logins.md).
* Para obtener más información sobre los usuarios de base de datos independiente, consulte [Usuarios de base de datos independiente: hacer que la base de datos sea portátil](https://msdn.microsoft.com/library/ff929188.aspx).
* Para obtener información sobre cómo usar y configurar la funcionalidad de replicación geográfica activa, consulte [Replicación geográfica activa para Azure SQL Database](sql-database-geo-replication-overview.md).
* Para obtener información sobre cómo utilizar la funcionalidad de restauración geográfica, consulte [Restauración geográfica](sql-database-recovery-using-backups.md#geo-restore)

