---
title: "Configuración de la seguridad de Azure SQL Database para recuperación ante desastres | Microsoft Docs"
description: "En este tema se explican las consideraciones de seguridad para configurar y administrar la seguridad después de la restauración de una base de datos o una conmutación por error en un servidor secundario ante la eventualidad de interrupción del centro de datos u otro desastre"
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
ms.openlocfilehash: de5e1732dab570b80692efcdd08e4ed2d8c98800
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configure-and-manage-azure-sql-database-security-for-geo-restore-or-failover"></a><span data-ttu-id="cac73-103">Configuración y administración de la seguridad de Azure SQL Database para la restauración geográfica o la conmutación por error</span><span class="sxs-lookup"><span data-stu-id="cac73-103">Configure and manage Azure SQL Database security for geo-restore or failover</span></span> 

> [!NOTE]
> <span data-ttu-id="cac73-104">La [replicación geográfica activa](sql-database-geo-replication-overview.md) está ahora disponible para todas las bases de datos en todos los niveles de servicio.</span><span class="sxs-lookup"><span data-stu-id="cac73-104">[Active geo-replication](sql-database-geo-replication-overview.md) is now available for all databases in all service tiers.</span></span>
>  

## <a name="overview-of-authentication-requirements-for-disaster-recovery"></a><span data-ttu-id="cac73-105">Información general sobre los requisitos de autenticación para la recuperación ante desastres</span><span class="sxs-lookup"><span data-stu-id="cac73-105">Overview of authentication requirements for disaster recovery</span></span>
<span data-ttu-id="cac73-106">En este tema se describen los requisitos de autenticación para configurar y controlar la [replicación geográfica activa](sql-database-geo-replication-overview.md) y los pasos necesarios para configurar el acceso de usuario a la base de datos secundaria.</span><span class="sxs-lookup"><span data-stu-id="cac73-106">This topic describes the authentication requirements to configure and control [active geo-replication](sql-database-geo-replication-overview.md) and the steps required to set up user access to the secondary database.</span></span> <span data-ttu-id="cac73-107">También se describe cómo habilitar el acceso a la base de datos recuperada después de utilizar la [georrestauración](sql-database-recovery-using-backups.md#geo-restore).</span><span class="sxs-lookup"><span data-stu-id="cac73-107">It also describes how enable access to the recovered database after using [geo-restore](sql-database-recovery-using-backups.md#geo-restore).</span></span> <span data-ttu-id="cac73-108">Para más información sobre opciones de recuperación, consulte [Información general sobre la continuidad empresarial](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="cac73-108">For more information on recovery options, see [Business Continuity Overview](sql-database-business-continuity.md).</span></span>

## <a name="disaster-recovery-with-contained-users"></a><span data-ttu-id="cac73-109">Recuperación ante desastres con usuarios contenidos</span><span class="sxs-lookup"><span data-stu-id="cac73-109">Disaster recovery with contained users</span></span>
<span data-ttu-id="cac73-110">A diferencia de los usuarios tradicionales, que deben asignarse a inicios de sesión en la base de datos maestra, un usuario independiente se administra completamente en la base de datos,</span><span class="sxs-lookup"><span data-stu-id="cac73-110">Unlike traditional users, which must be mapped to logins in the master database, a contained user is managed completely by the database itself.</span></span> <span data-ttu-id="cac73-111">lo que ofrece dos ventajas.</span><span class="sxs-lookup"><span data-stu-id="cac73-111">This has two benefits.</span></span> <span data-ttu-id="cac73-112">En el escenario de replicación geográfica, los usuarios pueden proceder a conectarse a la nueva base de datos principal o a la base de datos recuperada mediante georrestauración, sin ninguna configuración adicional, ya que la base de datos administra los usuarios.</span><span class="sxs-lookup"><span data-stu-id="cac73-112">In the disaster recovery scenario, the users can continue to connect to the new primary database or the database recovered using geo-restore without any additional configuration, because the database manages the users.</span></span> <span data-ttu-id="cac73-113">También existen ventajas potenciales de escalabilidad y rendimiento con esta configuración desde la perspectiva del inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="cac73-113">There are also potential scalability and performance benefits from this configuration from a login perspective.</span></span> <span data-ttu-id="cac73-114">Para obtener más información, vea [Usuarios de base de datos independiente - Conversión de la base de datos en portátil](https://msdn.microsoft.com/library/ff929188.aspx).</span><span class="sxs-lookup"><span data-stu-id="cac73-114">For more information, see [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span></span> 

<span data-ttu-id="cac73-115">El principal inconveniente es que la administración del proceso de recuperación ante desastres a escala es más compleja.</span><span class="sxs-lookup"><span data-stu-id="cac73-115">The main trade-off is that managing the disaster recovery process at scale is more challenging.</span></span> <span data-ttu-id="cac73-116">Si tiene varias bases de datos que usan el mismo inicio de sesión, el mantenimiento de las credenciales que usan los usuarios independientes en varias bases de datos puede invalidar las ventajas de los usuarios independientes.</span><span class="sxs-lookup"><span data-stu-id="cac73-116">When you have multiple databases that use the same login, maintaining the credentials using contained users in multiple databases may negate the benefits of contained users.</span></span> <span data-ttu-id="cac73-117">Por ejemplo, la directiva de rotación de contraseñas requiere que se realicen cambios constantemente en varias bases de datos en lugar de cambiar la contraseña para el inicio de sesión una vez en la base de datos maestra.</span><span class="sxs-lookup"><span data-stu-id="cac73-117">For example, the password rotation policy requires that changes be made consistently in multiple databases rather than changing the password for the login once in the master database.</span></span> <span data-ttu-id="cac73-118">Por este motivo, si tiene varias bases de datos que utilizan el mismo nombre de usuario y la misma contraseña, no se recomienda usar usuarios contenidos.</span><span class="sxs-lookup"><span data-stu-id="cac73-118">For this reason, if you have multiple databases that use the same user name and password, using contained users is not recommended.</span></span> 

## <a name="how-to-configure-logins-and-users"></a><span data-ttu-id="cac73-119">Configuración de inicios de sesión y de usuarios</span><span class="sxs-lookup"><span data-stu-id="cac73-119">How to configure logins and users</span></span>
<span data-ttu-id="cac73-120">Si usa inicios de sesión y usuarios (en lugar de usuarios contenidos), debe realizar pasos adicionales para asegurarse de que existan los mismos inicios de sesión en la base de datos maestra.</span><span class="sxs-lookup"><span data-stu-id="cac73-120">If you are using logins and users (rather than contained users), you must take extra steps to insure that the same logins exist in the master database.</span></span> <span data-ttu-id="cac73-121">En las secciones siguientes, se describen los pasos necesarios y otras consideraciones.</span><span class="sxs-lookup"><span data-stu-id="cac73-121">The following sections outline the steps involved and additional considerations.</span></span>

### <a name="set-up-user-access-to-a-secondary-or-recovered-database"></a><span data-ttu-id="cac73-122">Configuración del acceso de usuario a una base de datos secundaria o recuperada</span><span class="sxs-lookup"><span data-stu-id="cac73-122">Set up user access to a secondary or recovered database</span></span>
<span data-ttu-id="cac73-123">Para que la base de datos secundaria se pueda utilizar como base de datos secundaria de solo lectura y garantizar el acceso adecuado a la nueva base de datos principal o a la base de datos recuperada mediante la georrestauración, la base de datos maestra del servidor de destino debe tener la configuración de seguridad adecuada antes de la recuperación.</span><span class="sxs-lookup"><span data-stu-id="cac73-123">In order for the secondary database to be usable as a read-only secondary database, and to ensure proper access to the new primary database or the database recovered using geo-restore, the master database of the target server must have the appropriate security configuration in place before the recovery.</span></span>

<span data-ttu-id="cac73-124">Los permisos específicos para cada paso se describen más adelante en este tema.</span><span class="sxs-lookup"><span data-stu-id="cac73-124">The specific permissions for each step are described later in this topic.</span></span>

<span data-ttu-id="cac73-125">La preparación del acceso de usuario a una base de datos secundaria de replicación geográfica debe realizarse como parte de la configuración de replicación geográfica.</span><span class="sxs-lookup"><span data-stu-id="cac73-125">Preparing user access to a geo-replication secondary should be performed as part configuring geo-replication.</span></span> <span data-ttu-id="cac73-126">La preparación de acceso de usuario a las bases de datos georrestauradas debe realizarse en cualquier momento en que el servidor original esté en línea (por ejemplo, como parte de la obtención de detalles de recuperación ante desastres).</span><span class="sxs-lookup"><span data-stu-id="cac73-126">Preparing user access to the geo-restored databases should be performed at any time when the original server is online (e.g. as part of the DR drill).</span></span>

> [!NOTE]
> <span data-ttu-id="cac73-127">Si realiza una conmutación por error o la georrestauración en un servidor que no tiene configurado correctamente el acceso de inicio de sesión al mismo, se limitará a la cuenta de administrador del servidor.</span><span class="sxs-lookup"><span data-stu-id="cac73-127">If you fail over or geo-restore to a server that does not have properly configured logins, access to it will be limited to the server admin account.</span></span>
> 
> 

<span data-ttu-id="cac73-128">La configuración de los inicios de sesión en el servidor de destino implica los tres pasos descritos a continuación:</span><span class="sxs-lookup"><span data-stu-id="cac73-128">Setting up logins on the target server involves three steps outlined below:</span></span>

#### <a name="1-determine-logins-with-access-to-the-primary-database"></a><span data-ttu-id="cac73-129">1. Determinar los inicios de sesión con acceso a la base de datos principal:</span><span class="sxs-lookup"><span data-stu-id="cac73-129">1. Determine logins with access to the primary database:</span></span>
<span data-ttu-id="cac73-130">El primer paso del proceso es determinar qué inicios de sesión se deben duplicar en el servidor de destino.</span><span class="sxs-lookup"><span data-stu-id="cac73-130">The first step of the process is to determine which logins must be duplicated on the target server.</span></span> <span data-ttu-id="cac73-131">Esto se logra con un par de instrucciones SELECT, una en la base de datos maestra lógica del servidor de origen y otra, en la base de datos principal en sí.</span><span class="sxs-lookup"><span data-stu-id="cac73-131">This is accomplished with a pair of SELECT statements, one in the logical master database on the source server and one in the primary database itself.</span></span>

<span data-ttu-id="cac73-132">El administrador del servidor o un miembro del rol de servidor **LoginManager** son los únicos que pueden determinar los inicios de sesión en el servidor de origen con la siguiente instrucción SELECT.</span><span class="sxs-lookup"><span data-stu-id="cac73-132">Only the server admin or a member of the **LoginManager** server role can determine the logins on the source server with the following SELECT statement.</span></span> 

    SELECT [name], [sid] 
    FROM [sys].[sql_logins] 
    WHERE [type_desc] = 'SQL_Login'

<span data-ttu-id="cac73-133">Solo un miembro del rol de base de datos db_owner, el usuario dbo o el administrador del servidor pueden determinar todas las entidades de seguridad de usuario de base de datos en la base de datos principal.</span><span class="sxs-lookup"><span data-stu-id="cac73-133">Only a member of the db_owner database role, the dbo user, or server admin, can determine all of the database user principals in the primary database.</span></span>

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

#### <a name="2-find-the-sid-for-the-logins-identified-in-step-1"></a><span data-ttu-id="cac73-134">2. Buscar al SID de los inicios de sesión que identificó en el paso 1:</span><span class="sxs-lookup"><span data-stu-id="cac73-134">2. Find the SID for the logins identified in step 1:</span></span>
<span data-ttu-id="cac73-135">Al comparar los resultados de las consultas de la sección anterior y cotejar los SID, puede asignar el inicio de sesión de servidor a un usuario de base de datos.</span><span class="sxs-lookup"><span data-stu-id="cac73-135">By comparing the output of the queries from the previous section and matching the SIDs, you can map the server login to database user.</span></span> <span data-ttu-id="cac73-136">Los inicios de sesión que cuenten con un usuario de base de datos con un SID coincidente tienen acceso de usuario a esa base de datos como entidad de seguridad de usuario de base de datos.</span><span class="sxs-lookup"><span data-stu-id="cac73-136">Logins that have a database user with a matching SID have user access to that database as that database user principal.</span></span> 

<span data-ttu-id="cac73-137">La consulta siguiente se puede usar para ver todas las entidades de seguridad de usuario y sus SID en una base de datos.</span><span class="sxs-lookup"><span data-stu-id="cac73-137">The following query can be used to see all of the user principals and their SIDs in a database.</span></span> <span data-ttu-id="cac73-138">Solo un miembro del rol de servidor db_owner o el administrador del servidor pueden ejecutar esta consulta.</span><span class="sxs-lookup"><span data-stu-id="cac73-138">Only a member of the db_owner database role or server admin can run this query.</span></span>

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

> [!NOTE]
> <span data-ttu-id="cac73-139">Los usuarios de **INFORMATION_SCHEMA** y **sys** tienen SID *NULL* SID, mientras que el SID de **guest** es **0x00**.</span><span class="sxs-lookup"><span data-stu-id="cac73-139">The **INFORMATION_SCHEMA** and **sys** users have *NULL* SIDs, and the **guest** SID is **0x00**.</span></span> <span data-ttu-id="cac73-140">El SID de **dbo** puede empezar por *0x01060000000001648000000000048454* si el creador de la base de datos era el administrador del servidor en lugar de un miembro de **DbManager**.</span><span class="sxs-lookup"><span data-stu-id="cac73-140">The **dbo** SID may start with *0x01060000000001648000000000048454*, if the database creator was the server admin instead of a member of **DbManager**.</span></span>
> 
> 

#### <a name="3-create-the-logins-on-the-target-server"></a><span data-ttu-id="cac73-141">3. Crear los inicios de sesión en el servidor de destino:</span><span class="sxs-lookup"><span data-stu-id="cac73-141">3. Create the logins on the target server:</span></span>
<span data-ttu-id="cac73-142">El último paso consiste en ir al servidor o los servidores de destino y generar los inicios de sesión con los SID correspondientes.</span><span class="sxs-lookup"><span data-stu-id="cac73-142">The last step is to go to the target server, or servers, and generate the logins with the appropriate SIDs.</span></span> <span data-ttu-id="cac73-143">Esta es la sintaxis básica.</span><span class="sxs-lookup"><span data-stu-id="cac73-143">The basic syntax is as follows.</span></span>

    CREATE LOGIN [<login name>]
    WITH PASSWORD = <login password>,
    SID = <desired login SID>

> [!NOTE]
> <span data-ttu-id="cac73-144">Si desea conceder acceso de usuario a la base de datos secundaria, pero no a la principal, puede hacerlo modificando el inicio de sesión de usuario en el servidor principal con la sintaxis siguiente.</span><span class="sxs-lookup"><span data-stu-id="cac73-144">If you want to grant user access to the secondary, but not to the primary, you can do that by altering the user login on the primary server by using the following syntax.</span></span>
> 
> <span data-ttu-id="cac73-145">ALTER LOGIN <login name> DISABLE</span><span class="sxs-lookup"><span data-stu-id="cac73-145">ALTER LOGIN <login name> DISABLE</span></span>
> 
> <span data-ttu-id="cac73-146">DISABLE no cambia la contraseña, por lo que siempre puede habilitarlo si es necesario.</span><span class="sxs-lookup"><span data-stu-id="cac73-146">DISABLE doesn’t change the password, so you can always enable it if needed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="cac73-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cac73-147">Next steps</span></span>
* <span data-ttu-id="cac73-148">Para obtener más información sobre cómo administrar el acceso a la base de datos y los inicios de sesión, consulte [Seguridad de la Base de datos SQL: administrar la seguridad del inicio de sesión y el acceso a la base de datos](sql-database-manage-logins.md).</span><span class="sxs-lookup"><span data-stu-id="cac73-148">For more information on managing database access and logins, see [SQL Database security: Manage database access and login security](sql-database-manage-logins.md).</span></span>
* <span data-ttu-id="cac73-149">Para obtener más información sobre los usuarios de base de datos independiente, consulte [Usuarios de base de datos independiente: hacer que la base de datos sea portátil](https://msdn.microsoft.com/library/ff929188.aspx).</span><span class="sxs-lookup"><span data-stu-id="cac73-149">For more information on contained database users, see [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span></span>
* <span data-ttu-id="cac73-150">Para obtener información sobre cómo usar y configurar la funcionalidad de replicación geográfica activa, consulte [Replicación geográfica activa para Azure SQL Database](sql-database-geo-replication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cac73-150">For information about using and configuring active geo-replication, see [active geo-replication](sql-database-geo-replication-overview.md)</span></span>
* <span data-ttu-id="cac73-151">Para obtener información sobre cómo utilizar la funcionalidad de restauración geográfica, consulte [Restauración geográfica](sql-database-recovery-using-backups.md#geo-restore)</span><span class="sxs-lookup"><span data-stu-id="cac73-151">For information about using geo-restore, see [geo-restore](sql-database-recovery-using-backups.md#geo-restore)</span></span>

