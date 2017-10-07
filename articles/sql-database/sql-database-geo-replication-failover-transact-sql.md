---
title: "TSQL: inicio de una conmutación por error para Azure SQL Database | Microsoft Docs"
description: "Inicio de una conmutación por error planeada o no planeada para Base de datos SQL de Azure con Transact-SQL"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 5eb2d256-025d-4f5a-99d4-17f702b37f14
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 418953e044ba84ce758063d56a371af45d5cdfe1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="initiate-a-planned-or-unplanned-failover-for-azure-sql-database-with-transact-sql"></a>Inicio de una conmutación por error planeada o no planeada para Base de datos SQL de Azure con Transact-SQL

Este artículo muestra cómo tooa de conmutación por error tooinitiate base de datos SQL secundaria mediante Transact-SQL. replicación geográfica tooconfigure, consulte [configurar la replicación geográfica para la base de datos de SQL Azure](sql-database-geo-replication-transact-sql.md).

conmutación por error tooinitiate, necesita siguiente de hello:

* Un inicio de sesión es DBManager en hello principal
* Tiene db_ownership de hello base de datos local que se va a replicar geográficamente
* Estar DBManager en hello asociado servidores toowhich que va a configurar la replicación geográfica
* La versión más reciente de SQL Server Management Studio (SSMS).

> [!IMPORTANT]
> Se recomienda que siempre utilice Hola versión más reciente de Management Studio tooremain sincronizada con actualizaciones tooMicrosoft Azure y base de datos SQL. [Actualice SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).
>  

## <a name="initiate-a-planned-failover-promoting-a-secondary-database-toobecome-hello-new-primary"></a>Iniciar una conmutación por error planeada promover una base de datos secundaria toobecome Hola principal
Puede usar hello **ALTER DATABASE** instrucción toopromote una base de datos secundaria toobecome Hola principal de base de datos de un modo planeado, disminuir de nivel toobecome principal existente de hello una base de datos secundaria. Esta instrucción se ejecuta en la base de datos maestra de hello en el servidor lógico en la base de datos de SQL Azure de hello en qué Hola reside georreplicadas base de datos secundaria que se está promocionando. Esta funcionalidad está diseñada para conmutación por error planeada, como durante los ejercicios de hello recuperación ante desastres y requiere que esa base de datos principal de hello esté disponible.

comando de Hello realiza Hola siguiendo el flujo de trabajo:

1. Temporalmente modo de toosynchronous de replicación de conmutadores, provocando toobe de todas las transacciones pendientes vaciados toohello secundaria y bloqueo de todas las nuevas transacciones;
2. Conmutadores Hola roles de dos bases de datos hello en colaboración de replicación geográfica de Hola.  

Esta secuencia garantiza que Hola dos bases de datos se sincronizan antes de cambiar los roles de hello y, por tanto, se producirá ninguna pérdida de datos. Hay un breve período durante el cual ambas bases de datos no están disponibles (en orden de Hola de 0 segundos too25) mientras conmutación de roles de Hola. Si la base de datos principal de hello tiene varias bases de datos secundarias, comando Hola se automáticamente reconfigure Hola otro secundarias tooconnect toohello nuevo elemento principal.  toda operación de Hello tardará menos de un minuto toocomplete en circunstancias normales. Para más información, vea [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) y [Niveles de servicio](sql-database-service-tiers.md).

Usar hello siguiendo los pasos tooinitiate una conmutación por error planeada.

1. En Management Studio, conecte el servidor lógico en la base de datos de SQL Azure de toohello en el que reside una base de datos secundaria de replicación geográfica.
2. Abra la carpeta de bases de datos de hello, expanda hello **bases de datos de sistema** carpeta, el botón secundario en **maestro**y, a continuación, haga clic en **nueva consulta**.
3. Utilice Hola siguiente **ALTER DATABASE** rol principal de toohello de base de datos secundaria tooswitch de Hola de instrucción.
   
        ALTER DATABASE <MyDB> FAILOVER;
4. Haga clic en **Execute** consulta de hello toorun.

> [!NOTE]
> En raras ocasiones, es posible que la operación de hello no se puede completar y puede aparecer bloqueada. En este caso, usuario Hola puede ejecutar el comando para forzar la conmutación por error hello y Aceptar pérdida de datos.
> 
> 

## <a name="initiate-an-unplanned-failover-from-hello-primary-database-toohello-secondary-database"></a>Iniciar una conmutación por error no planeada de base de datos secundaria de hello base de datos principal toohello
Puede usar hello **ALTER DATABASE** instrucción toopromote una base de datos secundaria toobecome Hola principal de base de datos de forma no planeada para forzar la degradación de Hola de toobecome principal existente de hello una base de datos secundaria a la vez cuando Hola base de datos principal ya no está disponible. Esta instrucción se ejecuta en la base de datos maestra de hello en el servidor lógico en la base de datos de SQL Azure de hello en qué Hola reside georreplicadas base de datos secundaria que se está promocionando.

Esta funcionalidad está diseñada para la recuperación ante desastres cuando sea crucial la disponibilidad de restauración de base de datos de Hola y alguna pérdida de datos es aceptable. Cuando se invoca la conmutación por error forzada, Hola especifica la base de datos secundaria se convierte en la base de datos principal de hello inmediatamente y comienza a aceptar las transacciones de escritura. Tan pronto como base de datos principal Hola original es capaz de tooreconnect con esta nueva base de datos principal, se realiza una copia de seguridad incremental en la base de datos principal Hola original y base de datos principal Hola anterior se convierte en una base de datos secundaria para hello nueva base de datos principal; como consecuencia, es simplemente una réplica sincronizar de nuevo elemento principal Hola.

Sin embargo, porque el punto de restauración a un momento no se admite en bases de datos secundarias de hello, si desea que un usuario de hello datos toorecover confirmados toohello antigua base de datos principal que no se hubiera toohello nuevo principal base de datos replicada antes de hello forzada conmutación por error se ha producido, Hello usuario deberá tooengage compatibilidad toorecover se pierden datos.

Si la base de datos principal de hello tiene varias bases de datos secundarias, comando Hola se automáticamente reconfigure Hola otro secundarias tooconnect toohello nuevo elemento principal.

Usar hello siguiendo los pasos tooinitiate una conmutación por error no planeada.

1. En Management Studio, conecte el servidor lógico en la base de datos de SQL Azure de toohello en el que reside una base de datos secundaria de replicación geográfica.
2. Abra la carpeta de bases de datos de hello, expanda hello **bases de datos de sistema** carpeta, el botón secundario en **maestro**y, a continuación, haga clic en **nueva consulta**.
3. Utilice Hola siguiente **ALTER DATABASE** rol principal de toohello de base de datos secundaria tooswitch de Hola de instrucción.
   
        ALTER DATABASE <MyDB>   FORCE_FAILOVER_ALLOW_DATA_LOSS;
4. Haga clic en **Execute** consulta de hello toorun.

> [!NOTE]
> Si se emite el comando de hello cuando principal y secundaria en línea se convertirá en el principal antiguo Hola Hola nueva base de datos secundaria inmediatamente sin necesidad de sincronización de datos. Si está de hello principal pueden producirse las transacciones de confirmación cuando se emite el comando de hello alguna pérdida de datos.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
* Después de la conmutación por error, asegúrese de que los requisitos de autenticación de hello para el servidor y la base de datos se configuran en la nueva réplica principal de Hola. Para obtener más información, consulte [Administración de la seguridad de Base de datos SQL de Azure después de la recuperación ante desastres](sql-database-geo-replication-security-config.md).
* toolearn en la recuperación tras un desastre utilizando la replicación geográfica activa, incluidos los pasos de recuperación anteriores y posteriores a la recuperación y realizar una exploración de recuperación ante desastres, consulte [recuperación ante desastres](sql-database-disaster-recovery.md)
* Para ver una entrada de blog de Sasha Nosov sobre la replicación geográfica activa, consulte [Spotlight on new Geo-Replication capabilities](https://azure.microsoft.com/blog/spotlight-on-new-capabilities-of-azure-sql-database-geo-replication/)
* Para obtener información acerca de cómo diseñar en la nube aplicaciones toouse replicación geográfica activa, consulte [diseño de aplicaciones de nube para la continuidad del negocio con la replicación geográfica](sql-database-designing-cloud-solutions-for-disaster-recovery.md)
* Para saber cómo utilizar la replicación geográfica activa con los grupos elásticos, consulte [Estrategias de recuperación ante desastres para grupos elásticos](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md).
* Para ver una descripción general de la continuidad empresarial, consulte el artículo de [introducción a la continuidad empresarial con Azure SQL Database](sql-database-business-continuity.md).

