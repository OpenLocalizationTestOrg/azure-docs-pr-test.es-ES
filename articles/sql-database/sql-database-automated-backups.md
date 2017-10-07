---
title: "aaaAzure base de datos SQL automática con redundancia geográfica copias de seguridad | Documentos de Microsoft"
description: "SQL Database crea automáticamente una copia de seguridad local de la base de datos cada pocos minutos y usa almacenamiento con redundancia geográfica con acceso de lectura de Azure para proporcionar redundancia geográfica."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 3ee3d49d-16fa-47cf-a3ab-7b22aa491a8d
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/05/2017
ms.author: carlrab
ms.openlocfilehash: 8aff5356e8142707dd7cd2533a4aa5ea8fec866d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-automatic-sql-database-backups"></a>Más información sobre copias de seguridad automáticas de SQL Database

Base de datos de SQL y crea automáticamente copias de seguridad de base de datos utiliza redundancia geográfica tooprovide almacenamiento con redundancia geográfica de Azure con acceso de lectura (RA-GRS). Estas copias de seguridad se crean automáticamente y sin cargos adicionales. No es necesario toodo nada toomake a suceder. Las copias de seguridad de base de datos son una parte esencial de cualquier estrategia de recuperación ante desastres y continuidad del negocio, ya que protegen los datos de daños o eliminaciones accidentales. Si desea que las copias de seguridad de tookeep en su propio contenedor de almacenamiento puede configurar una directiva de retención de copia de seguridad a largo plazo. Para más información, consulte [retención a largo plazo](sql-database-long-term-retention.md).

## <a name="what-is-a-sql-database-backup"></a>¿Qué es una copia de seguridad de SQL Database?

Base de datos de SQL utiliza toocreate de tecnología de SQL Server [completa](https://msdn.microsoft.com/library/ms186289.aspx), [diferencial](https://msdn.microsoft.com/library/ms175526.aspx), y [registro de transacciones](https://msdn.microsoft.com/library/ms191429.aspx) copias de seguridad. copias de seguridad del registro de transacciones de Hello suele ocurrir cada 5-10 minutos, con frecuencia de hello en función de nivel de rendimiento de Hola y cantidad de actividad de la base de datos. Copias del registro de transacciones, con las copias de seguridad completas y diferenciales, le permiten toorestore un toohello de en un momento específico de base de datos tooa mismo servidor que hospeda la base de datos de Hola. Cuando se restaura una base de datos, Hola determina servicio qué completa, diferencial y copias de seguridad de registro de transacciones necesitan toobe restaurado.


Puede utilizar estas copias de seguridad para realizar lo siguiente:

* Restaurar una base de datos tooa en un momento dentro del período de retención de Hola. Esta operación creará una nueva base de datos en hello mismo servidor que la base de datos original de Hola.
* Restaurar un tiempo de toohello de base de datos eliminada que se haya eliminado o en cualquier momento dentro del período de retención de Hola. base de datos de Hello elimina sólo pueden restaurarse en hello mismo servidor donde se creó la base de datos original de Hola.
* Restaurar una región geográfica de tooanother de base de datos. Esto permite toorecover ante desastres geográfica cuando no se puede tener acceso a su servidor y base de datos. Crea una nueva base de datos en cualquier servidor existente en cualquier parte de Hola a todos. 
* Restaurar una base de datos desde una copia de seguridad específica guardada en el almacén de Azure Recovery Services. Esto le permite toorestore una versión anterior de la base de datos de hello toosatisfy una solicitud de cumplimiento o una versión anterior de la aplicación hello toorun. Consulte el tema sobre la [retención a largo plazo](sql-database-long-term-retention.md).
* tooperform una restauración, vea [restaurar la base de datos de copias de seguridad](sql-database-recovery-using-backups.md).

> [!NOTE]
> En el almacenamiento de Azure, término hello *replicación* hace referencia toocopying archivos desde una ubicación tooanother. De SQL *replicación de base de datos* hace referencia a bases de datos de tookeeping toomultiple secundarias sincronizadas con una base de datos principal. 
> 

## <a name="how-much-backup-storage-is-included-at-no-cost"></a>¿Cuánto almacenamiento de copia de seguridad se incluye sin costo?
Base de datos SQL permite hasta too200% de su almacenamiento de base de datos aprovisionado máximo como almacenamiento de copia de seguridad sin costo adicional alguno. Por ejemplo, si tiene una instancia de base de datos de tipo Estándar con un tamaño de base de datos aprovisionado de 250 GB, tendrá 500 GB para almacenar copias de seguridad sin costos adicionales. Si la base de datos supera Hola proporcionada almacenamiento de copia de seguridad, puede elegir el período de retención de hello tooreduce póngase en contacto con soporte técnico de Azure. Otra opción es toopay para el almacenamiento de copia de seguridad adicional que se factura a velocidad de hello estándar almacenamiento geográficamente redundante con acceso de lectura (RA-GRS). 

## <a name="how-often-do-backups-happen"></a>¿Con qué frecuencia se producen las copias de seguridad?
Las copias de seguridad de bases de datos completas se producen con una frecuencia semanal, las diferenciales tienden a llevarse a cabo en intervalos de pocas horas y las de registro de transacciones suelen realizarse cada 5-10 minutos. copia de seguridad completa Hola primera programada inmediatamente después de crea una base de datos. Normalmente se completa dentro de 30 minutos, pero puede tardar más tiempo cuando la base de datos de hello un tamaño considerable. Por ejemplo, copia de seguridad inicial de hello puede tardar más en una base de datos restaurada o una copia de la base de datos. Después de hello primera copia de seguridad completa, todas las copias de seguridad adicionales se programan automáticamente y administra en modo silencioso en segundo plano de Hola. control de tiempo exacta Hola de todas las copias de seguridad de base de datos está determinada por hello servicio de base de datos de SQL según equilibra Hola general cargas de trabajo del sistema. 

replicación geográfica del almacenamiento de copia de seguridad del Hola se produce en función de la programación de replicación de almacenamiento de Azure Hola.

## <a name="how-long-do-you-keep-my-backups"></a>¿Cuánto tiempo se mantienen las copias de seguridad?
Cada copia de seguridad de base de datos de SQL tiene un período de retención que se basa en hello [nivel de servicio](sql-database-service-tiers.md) de base de datos de Hola. período de retención de Hola para una base de datos en el:


* Nivel de servicio Básico: 7 días.
* Nivel de servicio Estándar: 35 días
* Nivel de servicio Premium: 35 días.

Si cambiar la base de datos estándar de Hola o tooBasic de niveles de servicio Premium, se guardan las copias de seguridad de Hola durante siete días. Todas las copias de seguridad existentes con una antigüedad de más de siete días ya no estarán disponibles. 

Si actualiza la base de datos de tooStandard de nivel de servicio básico de Hola o Premium, base de datos SQL mantiene copias de seguridad existentes hasta que se 35 días de antigüedad. Además, mantiene nuevas copias de seguridad que se producen durante 35 días.

Si elimina una base de datos, base de datos SQL mantiene las copias de seguridad de Hola Hola igual haría para una base de datos en línea. Por ejemplo, suponga que elimina una base de datos básica que tiene un período de retención de siete días. Una copia de seguridad con cuatro días de antigüedad se guarda durante tres días más.

> [!IMPORTANT]
> Si elimina hello Azure SQL server que hospeda las bases de datos SQL, todas las bases de datos que pertenecen toohello server también se elimina y no se puede recuperar. No puede restaurar un servidor eliminado.
> 

## <a name="how-tooextend-hello-backup-retention-period"></a>¿Cómo tooextend Hola backup período de retención?
Si la aplicación requiere que las copias de seguridad de hello están disponibles para el período de tiempo más largo puede ampliar el período de retención integrados de hello mediante la configuración de directiva de retención de copia de seguridad a largo plazo de Hola para bases de datos individuales (directiva de izquierda a derecha). Esto le permite período de retención de TI integrada de hello tooextend de años de 35 días tooup too10. Para más información, consulte [retención a largo plazo](sql-database-long-term-retention.md).

Una vez que agregue Hola LTR directiva tooa base de datos mediante el portal de Azure o API, copias de seguridad de base de datos completa semanal Hola será automáticamente copiado tooyour posee el servicio Almacén de copia de seguridad de Azure. Si la base de datos está cifrada con copias de seguridad TDE Hola automáticamente se cifran en reposo.  Hola almacén de servicios, eliminará automáticamente las copias de seguridad expirados según su marca de tiempo y Hola directiva de izquierda a derecha.  Por lo que no necesita programación de copia de seguridad de toomanage Hola o preocuparse acerca de la limpieza de Hola Hola archivos antiguos. Hola restauración API es compatible con el almacén de copias de seguridad almacenadas en hello siempre que sea el almacén de hello en Hola misma suscripción que la base de datos SQL. Puede usar Hola portal de Azure o PowerShell tooaccess estas copias de seguridad.

> [!TIP]
> Para un tooguide cómo, consulte [configurar y restauración de retención de copia de seguridad a largo plazo de base de datos de SQL Azure](sql-database-long-term-backup-retention-configure.md)
>

## <a name="are-backups-encrypted"></a>¿Se cifran las copias de seguridad?

Cuando TDE está habilitado para una instancia de Azure SQL Database, también se cifran las copias de seguridad. Todas las instancias nuevas de Azure SQL Database están configuradas con TDE habilitado de forma predeterminada. Para más información, vea [Cifrado de datos transparente con Azure SQL Database](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database).

## <a name="next-steps"></a>Pasos siguientes

- Las copias de seguridad de base de datos son una parte esencial de cualquier estrategia de recuperación ante desastres y continuidad del negocio, ya que protegen los datos de daños o eliminaciones accidentales. toolearn aproximadamente Hola otras soluciones de continuidad del negocio de base de datos de SQL Azure, consulte [información general sobre la continuidad de negocio](sql-database-business-continuity.md).
- toorestore tooa punto en el tiempo con hello portal de Azure, consulte [Restaurar base de datos tooa punto en el tiempo mediante el portal de Azure de hello](sql-database-recovery-using-backups.md).
- toorestore tooa punto en el tiempo con PowerShell, vea [Restaurar base de datos tooa punto en el tiempo con PowerShell](scripts/sql-database-restore-database-powershell.md).
- tooconfigure, administrar y restaurar desde la retención a largo plazo de copias de seguridad automatizadas en un almacén de servicios de recuperación de Azure con hello Azure portal, vea [retención de copia de seguridad a largo plazo de administrar mediante Hola portal de Azure](sql-database-long-term-backup-retention-configure.md).
- tooconfigure, administrar y restaurar desde la retención a largo plazo de copias de seguridad automatizadas en un almacén de servicios de recuperación de Azure con PowerShell, vea [administrar la retención de copia de seguridad a largo plazo con PowerShell](sql-database-long-term-backup-retention-configure.md).
