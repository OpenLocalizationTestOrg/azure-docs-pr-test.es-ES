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
# <a name="configure-and-manage-azure-sql-database-security-for-geo-restore-or-failover"></a><span data-ttu-id="35318-103">Configuración y administración de la seguridad de Azure SQL Database para la restauración geográfica o la conmutación por error</span><span class="sxs-lookup"><span data-stu-id="35318-103">Configure and manage Azure SQL Database security for geo-restore or failover</span></span> 

> [!NOTE]
> <span data-ttu-id="35318-104">La [replicación geográfica activa](sql-database-geo-replication-overview.md) está ahora disponible para todas las bases de datos en todos los niveles de servicio.</span><span class="sxs-lookup"><span data-stu-id="35318-104">[Active geo-replication](sql-database-geo-replication-overview.md) is now available for all databases in all service tiers.</span></span>
>  

## <a name="overview-of-authentication-requirements-for-disaster-recovery"></a><span data-ttu-id="35318-105">Información general sobre los requisitos de autenticación para la recuperación ante desastres</span><span class="sxs-lookup"><span data-stu-id="35318-105">Overview of authentication requirements for disaster recovery</span></span>
<span data-ttu-id="35318-106">Este tema describe Hola authentication requisitos tooconfigure y control [replicación geográfica activa](sql-database-geo-replication-overview.md) Hola pasos tooset requiere la base de datos de usuario acceso toohello secundaria.</span><span class="sxs-lookup"><span data-stu-id="35318-106">This topic describes hello authentication requirements tooconfigure and control [active geo-replication](sql-database-geo-replication-overview.md) and hello steps required tooset up user access toohello secondary database.</span></span> <span data-ttu-id="35318-107">También se describe cómo habilitar la base de datos de access toohello recuperado después de usar [georestauración](sql-database-recovery-using-backups.md#geo-restore).</span><span class="sxs-lookup"><span data-stu-id="35318-107">It also describes how enable access toohello recovered database after using [geo-restore](sql-database-recovery-using-backups.md#geo-restore).</span></span> <span data-ttu-id="35318-108">Para más información sobre opciones de recuperación, consulte [Información general sobre la continuidad empresarial](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="35318-108">For more information on recovery options, see [Business Continuity Overview](sql-database-business-continuity.md).</span></span>

## <a name="disaster-recovery-with-contained-users"></a><span data-ttu-id="35318-109">Recuperación ante desastres con usuarios contenidos</span><span class="sxs-lookup"><span data-stu-id="35318-109">Disaster recovery with contained users</span></span>
<span data-ttu-id="35318-110">A diferencia de usuarios tradicionales, que debe asignarse toologins en la base de datos maestra de hello, un usuario contenido se administra completamente Hola propia base de datos.</span><span class="sxs-lookup"><span data-stu-id="35318-110">Unlike traditional users, which must be mapped toologins in hello master database, a contained user is managed completely by hello database itself.</span></span> <span data-ttu-id="35318-111">lo que ofrece dos ventajas.</span><span class="sxs-lookup"><span data-stu-id="35318-111">This has two benefits.</span></span> <span data-ttu-id="35318-112">En el escenario de recuperación ante desastres de hello, los usuarios de hello pueden seguir tooconnect toohello nueva base de datos principal o base de datos de hello recuperado utilizando la restauración geográfica sin ninguna configuración adicional, porque los usuarios de Hola encarga de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="35318-112">In hello disaster recovery scenario, hello users can continue tooconnect toohello new primary database or hello database recovered using geo-restore without any additional configuration, because hello database manages hello users.</span></span> <span data-ttu-id="35318-113">También existen ventajas potenciales de escalabilidad y rendimiento con esta configuración desde la perspectiva del inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="35318-113">There are also potential scalability and performance benefits from this configuration from a login perspective.</span></span> <span data-ttu-id="35318-114">Para obtener más información, vea [Usuarios de base de datos independiente - Conversión de la base de datos en portátil](https://msdn.microsoft.com/library/ff929188.aspx).</span><span class="sxs-lookup"><span data-stu-id="35318-114">For more information, see [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span></span> 

<span data-ttu-id="35318-115">ventajas y desventajas de Hello principal son que es más difícil administrar el proceso de recuperación ante desastres de Hola a escala.</span><span class="sxs-lookup"><span data-stu-id="35318-115">hello main trade-off is that managing hello disaster recovery process at scale is more challenging.</span></span> <span data-ttu-id="35318-116">Si tiene varias bases de datos ese Hola uso mismo inicio de sesión, mantenimiento de las credenciales de hello con contenidos a los usuarios en varias bases de datos pueden invalidar ventajas de Hola de usuarios contenidos.</span><span class="sxs-lookup"><span data-stu-id="35318-116">When you have multiple databases that use hello same login, maintaining hello credentials using contained users in multiple databases may negate hello benefits of contained users.</span></span> <span data-ttu-id="35318-117">Por ejemplo, directiva de rotación de hello contraseña requiere que se realizan cambios coherente en varias bases de datos en lugar de cambiar la contraseña de inicio de sesión de Hola Hola una vez en la base de datos maestra Hola.</span><span class="sxs-lookup"><span data-stu-id="35318-117">For example, hello password rotation policy requires that changes be made consistently in multiple databases rather than changing hello password for hello login once in hello master database.</span></span> <span data-ttu-id="35318-118">Por este motivo, si tiene varias bases de datos que use Hola mismo nombre de usuario y la contraseña, no se recomienda utilizar usuarios contenidos.</span><span class="sxs-lookup"><span data-stu-id="35318-118">For this reason, if you have multiple databases that use hello same user name and password, using contained users is not recommended.</span></span> 

## <a name="how-tooconfigure-logins-and-users"></a><span data-ttu-id="35318-119">¿Cómo tooconfigure inicios de sesión y usuarios</span><span class="sxs-lookup"><span data-stu-id="35318-119">How tooconfigure logins and users</span></span>
<span data-ttu-id="35318-120">Si usas los inicios de sesión y usuarios (en lugar de usuarios contenidos), debe seguir tooinsure pasos adicionales que Hola mismos inicios de sesión existen en la base de datos maestra de Hola.</span><span class="sxs-lookup"><span data-stu-id="35318-120">If you are using logins and users (rather than contained users), you must take extra steps tooinsure that hello same logins exist in hello master database.</span></span> <span data-ttu-id="35318-121">Hello siguientes secciones presentan consideraciones implicados y adicional de pasos de Hola.</span><span class="sxs-lookup"><span data-stu-id="35318-121">hello following sections outline hello steps involved and additional considerations.</span></span>

### <a name="set-up-user-access-tooa-secondary-or-recovered-database"></a><span data-ttu-id="35318-122">Establecer usuario acceso tooa secundaria o recuperada base de datos</span><span class="sxs-lookup"><span data-stu-id="35318-122">Set up user access tooa secondary or recovered database</span></span>
<span data-ttu-id="35318-123">Para hello toobe de base de datos secundaria puede usar como una base de datos secundaria de solo lectura y tooensure el acceso adecuado toohello nuevo principal Hola o base de datos de base de datos recuperar utilizando la restauración geográfica, Hola maestra base de datos del servidor de destino de hello debe tener Hola configuración de seguridad apropiada en su lugar antes de la recuperación de Hola.</span><span class="sxs-lookup"><span data-stu-id="35318-123">In order for hello secondary database toobe usable as a read-only secondary database, and tooensure proper access toohello new primary database or hello database recovered using geo-restore, hello master database of hello target server must have hello appropriate security configuration in place before hello recovery.</span></span>

<span data-ttu-id="35318-124">permisos específicos de Hola para cada paso se describen más adelante en este tema.</span><span class="sxs-lookup"><span data-stu-id="35318-124">hello specific permissions for each step are described later in this topic.</span></span>

<span data-ttu-id="35318-125">Preparar tooa de acceso de usuario debe realizarse la replicación geográfica secundaria como parte de la configuración de replicación geográfica.</span><span class="sxs-lookup"><span data-stu-id="35318-125">Preparing user access tooa geo-replication secondary should be performed as part configuring geo-replication.</span></span> <span data-ttu-id="35318-126">Preparación de acceso de usuario restaurado geográfica de toohello las bases de datos debe realizarse en cualquier momento al servidor original de hello está en línea (por ejemplo, como parte de obtención de detalles de recuperación ante desastres de hello).</span><span class="sxs-lookup"><span data-stu-id="35318-126">Preparing user access toohello geo-restored databases should be performed at any time when hello original server is online (e.g. as part of hello DR drill).</span></span>

> [!NOTE]
> <span data-ttu-id="35318-127">Si se produce un error sobre o la restauración geográfica tooa al servidor no tiene inicios de sesión configuradas correctamente, tooit de acceso será limitado toohello cuenta de administrador de servidor.</span><span class="sxs-lookup"><span data-stu-id="35318-127">If you fail over or geo-restore tooa server that does not have properly configured logins, access tooit will be limited toohello server admin account.</span></span>
> 
> 

<span data-ttu-id="35318-128">Configurar inicios de sesión en el servidor de destino de hello implica tres pasos que se describen a continuación:</span><span class="sxs-lookup"><span data-stu-id="35318-128">Setting up logins on hello target server involves three steps outlined below:</span></span>

#### <a name="1-determine-logins-with-access-toohello-primary-database"></a><span data-ttu-id="35318-129">1. Determinar inicios de sesión con la base de datos de access toohello principal:</span><span class="sxs-lookup"><span data-stu-id="35318-129">1. Determine logins with access toohello primary database:</span></span>
<span data-ttu-id="35318-130">Hola primer paso del proceso de hello es toodetermine qué inicios de sesión se deben duplicar en el servidor de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="35318-130">hello first step of hello process is toodetermine which logins must be duplicated on hello target server.</span></span> <span data-ttu-id="35318-131">Esto se logra con un par de instrucciones SELECT, una en hello lógico base de datos maestra en el servidor de origen de Hola y de hello principal propia base de datos.</span><span class="sxs-lookup"><span data-stu-id="35318-131">This is accomplished with a pair of SELECT statements, one in hello logical master database on hello source server and one in hello primary database itself.</span></span>

<span data-ttu-id="35318-132">Hola solo el administrador del servidor o un miembro de hello **LoginManager** rol de servidor puede determinar los inicios de sesión de hello en el servidor de origen de hello con hello después de la instrucción SELECT.</span><span class="sxs-lookup"><span data-stu-id="35318-132">Only hello server admin or a member of hello **LoginManager** server role can determine hello logins on hello source server with hello following SELECT statement.</span></span> 

    SELECT [name], [sid] 
    FROM [sys].[sql_logins] 
    WHERE [type_desc] = 'SQL_Login'

<span data-ttu-id="35318-133">Sólo un miembro del rol de base de datos db_owner hello, un usuario de dbo de Hola o administrador del servidor, puede determinar todas Hola entidades de usuario de base de datos en la base de datos principal de Hola de.</span><span class="sxs-lookup"><span data-stu-id="35318-133">Only a member of hello db_owner database role, hello dbo user, or server admin, can determine all of hello database user principals in hello primary database.</span></span>

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

#### <a name="2-find-hello-sid-for-hello-logins-identified-in-step-1"></a><span data-ttu-id="35318-134">2. Encontrar Hola SID para los inicios de sesión de hello identificados en el paso 1:</span><span class="sxs-lookup"><span data-stu-id="35318-134">2. Find hello SID for hello logins identified in step 1:</span></span>
<span data-ttu-id="35318-135">Comparando la salida de hello de consultas de hello de la sección anterior de Hola y Hola coincidente SID, puede asignar el usuario de toodatabase de inicio de sesión de servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="35318-135">By comparing hello output of hello queries from hello previous section and matching hello SIDs, you can map hello server login toodatabase user.</span></span> <span data-ttu-id="35318-136">Inicios de sesión que tienen un usuario de base de datos con un SID coincidente tienen base de datos de usuario acceso toothat como ese usuario de base de datos principal.</span><span class="sxs-lookup"><span data-stu-id="35318-136">Logins that have a database user with a matching SID have user access toothat database as that database user principal.</span></span> 

<span data-ttu-id="35318-137">Hello consulta siguiente puede ser usado toosee todas las entidades de seguridad del usuario de Hola y sus SID en una base de datos.</span><span class="sxs-lookup"><span data-stu-id="35318-137">hello following query can be used toosee all of hello user principals and their SIDs in a database.</span></span> <span data-ttu-id="35318-138">Sólo un miembro de Hola db_owner, base de datos servidor o el rol de administrador puede ejecutar esta consulta.</span><span class="sxs-lookup"><span data-stu-id="35318-138">Only a member of hello db_owner database role or server admin can run this query.</span></span>

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

> [!NOTE]
> <span data-ttu-id="35318-139">Hola **INFORMATION_SCHEMA** y **sys** los usuarios tienen *NULL* hello y SID **invitado** SID es **0 x 00**.</span><span class="sxs-lookup"><span data-stu-id="35318-139">hello **INFORMATION_SCHEMA** and **sys** users have *NULL* SIDs, and hello **guest** SID is **0x00**.</span></span> <span data-ttu-id="35318-140">Hola **dbo** SID puede empezar por *0 x 01060000000001648000000000048454*, si es de creador de base de datos de Hola Hola administrador del servidor en lugar de un miembro de **DbManager**.</span><span class="sxs-lookup"><span data-stu-id="35318-140">hello **dbo** SID may start with *0x01060000000001648000000000048454*, if hello database creator was hello server admin instead of a member of **DbManager**.</span></span>
> 
> 

#### <a name="3-create-hello-logins-on-hello-target-server"></a><span data-ttu-id="35318-141">3. Crear inicios de sesión de hello en el servidor de destino de hello:</span><span class="sxs-lookup"><span data-stu-id="35318-141">3. Create hello logins on hello target server:</span></span>
<span data-ttu-id="35318-142">Hello último paso es el servidor de destino de toogo toohello, o los servidores y generar los inicios de sesión de hello con hello adecuados SID.</span><span class="sxs-lookup"><span data-stu-id="35318-142">hello last step is toogo toohello target server, or servers, and generate hello logins with hello appropriate SIDs.</span></span> <span data-ttu-id="35318-143">sintaxis básica de Hello es como sigue.</span><span class="sxs-lookup"><span data-stu-id="35318-143">hello basic syntax is as follows.</span></span>

    CREATE LOGIN [<login name>]
    WITH PASSWORD = <login password>,
    SID = <desired login SID>

> [!NOTE]
> <span data-ttu-id="35318-144">Si desea toogrant usuario acceso toohello base de datos secundaria, pero no toohello principal, puede hacerlo alterando el inicio de sesión de usuario de hello en el servidor principal de hello mediante el uso de hello según la sintaxis.</span><span class="sxs-lookup"><span data-stu-id="35318-144">If you want toogrant user access toohello secondary, but not toohello primary, you can do that by altering hello user login on hello primary server by using hello following syntax.</span></span>
> 
> <span data-ttu-id="35318-145">ALTER LOGIN <login name> DISABLE</span><span class="sxs-lookup"><span data-stu-id="35318-145">ALTER LOGIN <login name> DISABLE</span></span>
> 
> <span data-ttu-id="35318-146">DISABLE no cambia la contraseña de hello, por lo que siempre puede habilitar si es necesario.</span><span class="sxs-lookup"><span data-stu-id="35318-146">DISABLE doesn’t change hello password, so you can always enable it if needed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="35318-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="35318-147">Next steps</span></span>
* <span data-ttu-id="35318-148">Para obtener más información sobre cómo administrar el acceso a la base de datos y los inicios de sesión, consulte [Seguridad de la Base de datos SQL: administrar la seguridad del inicio de sesión y el acceso a la base de datos](sql-database-manage-logins.md).</span><span class="sxs-lookup"><span data-stu-id="35318-148">For more information on managing database access and logins, see [SQL Database security: Manage database access and login security](sql-database-manage-logins.md).</span></span>
* <span data-ttu-id="35318-149">Para obtener más información sobre los usuarios de base de datos independiente, consulte [Usuarios de base de datos independiente: hacer que la base de datos sea portátil](https://msdn.microsoft.com/library/ff929188.aspx).</span><span class="sxs-lookup"><span data-stu-id="35318-149">For more information on contained database users, see [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span></span>
* <span data-ttu-id="35318-150">Para obtener información sobre cómo usar y configurar la funcionalidad de replicación geográfica activa, consulte [Replicación geográfica activa para Azure SQL Database](sql-database-geo-replication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="35318-150">For information about using and configuring active geo-replication, see [active geo-replication](sql-database-geo-replication-overview.md)</span></span>
* <span data-ttu-id="35318-151">Para obtener información sobre cómo utilizar la funcionalidad de restauración geográfica, consulte [Restauración geográfica](sql-database-recovery-using-backups.md#geo-restore)</span><span class="sxs-lookup"><span data-stu-id="35318-151">For information about using geo-restore, see [geo-restore](sql-database-recovery-using-backups.md#geo-restore)</span></span>

