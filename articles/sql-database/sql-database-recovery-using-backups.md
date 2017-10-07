---
title: una base de datos de SQL Azure desde una copia de seguridad aaaRestore | Documentos de Microsoft
description: "Obtenga información acerca de la restauración en un momento, que le permite tooroll back un punto anterior de tooa de base de datos de SQL Azure en tiempo de espera (too35 días)."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: monicar
ms.assetid: fd1d334d-a035-4a55-9446-d1cf750d9cf7
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: carlrab
ms.openlocfilehash: 84ecc306a2072445c10dbf1e9d7cf3d1b43860cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="recover-an-azure-sql-database-using-automated-database-backups"></a>Recuperación de una Base de datos SQL de Azure mediante copias de seguridad automatizadas
SQL Database proporciona estas opciones para la recuperación de bases de datos mediante [copias de seguridad automatizadas de la base de datos](sql-database-automated-backups.md) y [copias de seguridad en retención a largo plazo](sql-database-long-term-retention.md). Puede restaurar de una copia de seguridad de base de datos a:

* Una nueva base de datos Hola recuperado del mismo servidor lógico tooa especifica momento dentro del período de retención de Hola. 
* Una base de datos de hello mismo servidor lógico recupera toohello tiempo de eliminación para una base de datos eliminada.
* Una base de datos en cualquier servidor lógico en cualquier región recupera toohello punto de hello últimas copias de seguridad diarias en almacenamiento de blobs de replicación geográfica (RA-GRS).

> [!IMPORTANT]
> Durante la restauración, no se puede sobrescribir la base de datos existente.
>

También puede usar [automatizada de copias de seguridad de base de datos](sql-database-automated-backups.md) toocreate una [copiar base de datos](sql-database-copy.md) en cualquier servidor lógico en cualquier región. 

## <a name="recovery-time"></a>Tiempo de recuperación
Hola toorestore de tiempo de recuperación una base de datos con copias de seguridad de base de datos automatizada se ve afectado por diversos factores: 

* tamaño de Hola de base de datos de Hola
* nivel de rendimiento de Hola de base de datos de Hola
* número de Hola de registros de transacciones implicados
* cantidad de Hola de actividad que necesita toobe reproduce punto de restauración de toorecover toohello
* ancho de banda de red de Hello si Restaurar hello es tooa otra región 
* número de Hola de solicitudes de restauración simultáneas que se procesan en la región de destino de Hola. 
  
  Para una base de datos muy grande o active restauración Hola puede tardar varias horas. Si hay una interrupción prolongada en una región, es posible que haya un gran número de solicitudes de restauración geográfica que se procesan en otras regiones. Cuando hay muchas solicitudes, puede aumentar el tiempo de recuperación de Hola para bases de datos en dicha región. La mayoría de las restauraciones de bases de datos dura unas 12 horas.
  
No hay ninguna restauración masiva de toodo de funcionalidad integrada. Hola [base de datos de SQL Azure: recuperación de servidor completa](https://gallery.technet.microsoft.com/Azure-SQL-Database-Full-82941666) script es un ejemplo de una manera de realizar esta tarea.

> [!IMPORTANT]
> toorecover utilizando copias de seguridad automáticas, debe ser miembro del rol de colaborador de SQL Server de hello en la suscripción de Hola o ser propietario de la suscripción de Hola. Puede recuperar con hello portal de Azure, PowerShell o API de REST de Hola. No puede utilizar Transact-SQL. 
> 

## <a name="point-in-time-restore"></a>Restauración a un momento dado

Puede restaurar una base de datos existente tooan anterior al momento dado como una nueva base de datos Hola mismo servidor lógico mediante Hola portal de Azure, [PowerShell](https://docs.microsoft.com/en-us/powershell/module/azurerm.sql/restore-azurermsqldatabase), o hello [API de REST](https://msdn.microsoft.com/library/azure/mt163685.aspx). 

> [!TIP]
> Para obtener un script de PowerShell de ejemplo que muestra cómo tooperform una restauración en el momento de una base de datos, vea [restaurar una base de datos SQL con PowerShell](scripts/sql-database-restore-database-powershell.md).
>

base de datos de Hello puede ser restaurada tooany nivel de servicio o de rendimiento y como una sola base de datos o en un grupo elástico. Asegúrese de tiene recursos suficientes en el servidor lógico de Hola o en hello grupo elástico toowhich va a restaurar base de datos de Hola. Una vez completado, Hola Restaurar base de datos es normal, totalmente accesible en línea. base de datos de Hello restaurado se cobra a la tarifa normal en función de su nivel de rendimiento y de nivel de servicio. No se producen cargos hasta que se complete la restauración de base de datos de Hola.

Por lo general restaurar una base de datos tooan punto anteriormente para fines de recuperación. Al hacerlo, puede tratar Hola Restaurar base de datos como sustituto de la base de datos original de Hola o usarlo tooretrieve datos de y, a continuación, actualizar la base de datos original de Hola. 

* ***Reemplazo de la base de datos:*** si la base de datos de hello restaurar está pensado como un reemplazo para la base de datos original de hello, debe comprobar el nivel de rendimiento de Hola o nivel de servicio son adecuado y escalar la base de datos de hello si es necesario. Puede cambiar el nombre de base de datos original de hello y, a continuación, asigne Hola Restaurar base de datos Hola original nombre mediante el comando ALTER DATABASE de hello en T-SQL. 
* ***Recuperación de datos:*** si tiene previsto tooretrieve datos de toorecover de hello Restaurar base de datos de un error del usuario o aplicación, necesita toowrite y ejecutar Hola necesarios recuperación scripts tooextract datos desde Hola Restaurar base de datos toohello base de datos original. Aunque la operación de restauración de hello puede tardar un toocomplete mucho tiempo, es visible en la lista de bases de datos de Hola a lo largo del proceso de restauración de Hola Hola Restaurar base de datos. Si elimina la base de datos de Hola durante la restauración de hello, se cancela la operación de restauración de hello y no se le cobrará por base de datos de hello no se completó la restauración de Hola. 

### <a name="azure-portal"></a>Azure Portal

toorecover tooa punto en el tiempo mediante Hola portal de Azure, página de hello abierto para la base de datos y haga clic en **restaurar** en la barra de herramientas de Hola.

![restauración a un momento dado](./media/sql-database-recovery-using-backups/point-in-time-recovery.png)

## <a name="deleted-database-restore"></a>Restauración de la base de datos eliminada
Puede restaurar una hora de eliminación de base de datos eliminada toohello para una base de datos eliminada en hello mismo servidor lógico mediante Hola portal de Azure, [PowerShell](https://docs.microsoft.com/en-us/powershell/module/azurerm.sql/restore-azurermsqldatabase), o hello [REST (createMode = restaurar)](https://msdn.microsoft.com/library/azure/mt163685.aspx). 

> [!TIP]
> Para obtener un ejemplo de PowerShell de script que se muestra cómo toorestore una base de datos eliminada, consulte [restaurar una base de datos SQL con PowerShell](scripts/sql-database-restore-database-powershell.md).
>

> [!IMPORTANT]
> Si elimina una instancia de servidor de Azure SQL Database, todas sus bases de datos también se eliminan y no se pueden recuperar. En estos momentos no es posible restaurar un servidor eliminado.
> 

### <a name="azure-portal"></a>Azure Portal

toorecover eliminado la base de datos durante su [período de retención](sql-database-service-tiers.md) Hola portal de Azure, página de hello abierto para el servidor y en el área de operaciones de hello, haga clic en **elimina las bases de datos**.

![restauración-base de datos-eliminada-1](./media/sql-database-recovery-using-backups/deleted-database-restore-1.png)


![restauración-base de datos-eliminada-2](./media/sql-database-recovery-using-backups/deleted-database-restore-2.png)

## <a name="geo-restore"></a>Restauración geográfica
Puede restaurar una base de datos SQL en cualquier servidor en cualquier región de Azure de hello más reciente a una replicación geográfica completas y diferenciales copias de seguridad. Restauración geográfica usa una copia de seguridad con redundancia geográfica como su origen y puede ser toorecover usado, una base de datos, incluso si la base de datos de Hola o centro de datos es inaccesible debido tooan interrupción. 

La restauración geográfica es recovery, opción predeterminada hello cuando la base de datos no está disponible debido a un incidente en la región de Hola donde se hospeda la base de datos de Hola. Si un incidente a gran escala en los resultados de una región de falta de disponibilidad de la aplicación de base de datos, puede restaurar una base de datos del servidor de tooa de las copias de seguridad de replicación geográfica de hello en ninguna otra región. Hay un retraso entre cuando se realiza una copia de seguridad diferencial y cuándo es tooan de replicación geográfica Azure blob en una región distinta. Este retraso puede ser la hora de tooan, por lo tanto, si se produce un desastre, puede haber una pérdida de datos de hora tooone. Hola siguientes ilustración muestra restauración de base de datos de Hola de hello última copia de seguridad disponible en otra región.

![Restauración geográfica](./media/sql-database-geo-restore/geo-restore-2.png)

> [!TIP]
> Para obtener un ejemplo de PowerShell de script que se muestra cómo tooperform una restauración geográfica, consulte [restaurar una base de datos SQL con PowerShell](scripts/sql-database-restore-database-powershell.md).
> 

Actualmente no se admite la restauración a un momento dad en una base de datos geográfica secundaria. La restauración a un momento dado solo puede realizarse en una base de datos principal. Para obtener información detallada sobre el uso de la restauración geográfica toorecover desde una interrupción, consulte [recuperarse de una interrupción](sql-database-disaster-recovery.md).

> [!IMPORTANT]
> Recuperación desde copias de seguridad es hello más básica de desastre Hola Hola a soluciones de recuperación disponibles en la base de datos de SQL con un RPO más largo y tiempo de recuperación de estimación (ERT). Para las soluciones que emplean bases de datos Básico, la restauración geográfica suele ser una solución de recuperación ante desastres razonable con un ERT de 12 horas. En lo que respecta a las soluciones que utilizan bases de datos Estándar o Premium más grandes que precisan tiempos de recuperación más cortos, sería conveniente considerar la posibilidad de usar la [replicación geográfica activa](sql-database-geo-replication-overview.md). Replicación geográfica activa ofrece un mucho menor RPO y ERT ya que solo requiere iniciar un elemento secundario de conmutación por error tooa replicada de manera continuada. Para obtener más información sobre las opciones de continuidad empresarial, vea [este artículo](sql-database-business-continuity.md).
> 

### <a name="azure-portal"></a>Azure Portal

toogeo restaurar una base de datos durante su [período de retención](sql-database-service-tiers.md) con hello portal de Azure, abrir la página de bases de datos SQL de Hola y, a continuación, haga clic en **agregar**. Hola **Select origen** cuadro de texto, seleccione **copia de seguridad**. Especificar copia de seguridad de Hola de qué recovery de hello tooperform en la región de Hola y en el servidor de Hola de su elección. 

## <a name="programmatically-performing-recovery-using-automated-backups"></a>Recuperación mediante programación con copias de seguridad automatizadas
Como se explicó anteriormente, además toohello portal de Azure, recuperación de base de datos se puede realizar mediante programación con Azure PowerShell u Hola API de REST. Hola las tablas siguientes describe los conjunto Hola de comandos disponibles.

### <a name="powershell"></a>PowerShell
| Cmdlet | Descripción |
| --- | --- |
| [Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase) |Obtiene una o más bases de datos. |
| [Get-AzureRMSqlDeletedDatabaseBackup](/powershell/module/azurerm.sql/get-azurermsqldeleteddatabasebackup) | Obtiene una base de datos eliminada que se puede restaurar. |
| [Get-AzureRmSqlDatabaseGeoBackup](/powershell/module/azurerm.sql/get-azurermsqldatabasegeobackup) |Obtiene una copia de seguridad con redundancia geográfica de una base de datos. |
| [Restore-AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase) |Restaura una Base de datos SQL. |
|  | |

### <a name="rest-api"></a>API de REST
| API | Descripción |
| --- | --- |
| [REST (createMode=Recovery)](https://msdn.microsoft.com/library/azure/mt163685.aspx) |Restaura una base de datos. |
| [Obtener el estado de creación o actualización de la base de datos](https://msdn.microsoft.com/library/azure/mt643934.aspx) |Estado de hello devuelve durante una operación de restauración |
|  | |

## <a name="summary"></a>Resumen
Las copias de seguridad automáticas protegen las bases de datos de los errores de usuario y de aplicación, la eliminación accidental de la base de datos y las interrupciones prolongadas. Esta funcionalidad integrada está disponible para todos los niveles de servicio y niveles de rendimiento. 

## <a name="next-steps"></a>Pasos siguientes
* Para obtener una descripción general y los escenarios de la continuidad empresarial, consulte [Continuidad empresarial con Base de datos SQL de Azure](sql-database-business-continuity.md)
* toolearn acerca de las copias de seguridad de base de datos de SQL de Azure automatizada, vea [copias de seguridad automáticas de base de datos SQL](sql-database-automated-backups.md)
* toolearn acerca de la retención de copia de seguridad a largo plazo, vea [retención de copia de seguridad a largo plazo](sql-database-long-term-retention.md)
* tooconfigure, administrar y restaurar desde la retención a largo plazo de copias de seguridad automatizadas en un almacén de servicios de recuperación de Azure con hello Azure portal, vea [retención de una copia de seguridad de configuración y el uso a largo plazo](sql-database-long-term-backup-retention-configure.md). 
* toolearn acerca de las opciones de recuperación más rápidos, consulte [replicación geográfica activa](sql-database-geo-replication-overview.md)  
