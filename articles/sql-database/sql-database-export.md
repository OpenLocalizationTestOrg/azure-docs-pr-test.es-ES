---
title: aaaExport un archivo BACPAC de tooa de base de datos SQL de Azure | Documentos de Microsoft
description: Exportar un archivo BACPAC tooa de base de datos de SQL Azure mediante Hola Portal de Azure
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 41d63a97-37db-4e40-b652-77c2fd1c09b7
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.date: 06/15/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: cb3b4227318e0fd2114529c86c9792615fe7fd1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="export-an-azure-sql-database-tooa-bacpac-file"></a>Exportar un archivo BACPAC de tooa de base de datos de SQL Azure

Cuando necesite tooexport una base de datos para el archivado o para la plataforma de tooanother móvil, puede exportar tooa de esquema y los datos de la base de datos de hello [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) archivo. Un archivo BACPAC es un archivo ZIP con una extensión de BACPAC que contiene los metadatos de Hola y los datos de una base de datos de SQL Server. Un archivo BACPAC se puede almacenar en Azure Blob Storage o en una ubicación local y, luego, volver a importarlo en Azure SQL Database o en una instalación local de SQL Server. 

> [!IMPORTANT] 
> La exportación automática de Azure SQL Database se retiró el 1 de marzo de 2017. Puede usar [retención de copia de seguridad a largo plazo](sql-database-long-term-retention.md
) o [automatización de Azure](https://github.com/Microsoft/azure-docs-pr/blob/2461f706f8fc1150e69312098640c0676206a531/articles/automation/automation-intro.md) tooperiodically archivo SQL bases de datos mediante PowerShell según la programación de tooa de su elección. Para obtener un ejemplo, descargar hello [script de PowerShell de ejemplo](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-automation-automated-export) desde Github.
>

## <a name="considerations-when-exporting-an-azure-sql-database"></a>Consideraciones al exportar una base de datos Azure SQL Database

* Para una exportación toobe transaccionalmente coherente, debe asegurarse de que no se está produciendo ninguna actividad de escritura durante la exportación de hello, o que se va a exportar desde un [copia transaccionalmente coherente](sql-database-copy.md) de la base de datos de SQL Azure.
* Si va a exportar tooblob almacenamiento, tamaño máximo de Hola de un archivo BACPAC es de 200 GB. tooarchive tamaño del archivo de BACPAC, exportar toolocal almacenamiento.
* No se admite la exportación de un almacenamiento premium BACPAC archivo tooAzure usando métodos de hello descritos en este artículo.
* Si la operación de exportación de Hola de base de datos de SQL Azure supera 20 horas, se puede cancelar. rendimiento de tooincrease durante la exportación, puede:
  * Aumentar temporalmente el nivel de servicio.
  * Dejará de todos los de lectura y escritura actividad durante la exportación de Hola.
  * Use un [índice agrupado](https://msdn.microsoft.com/library/ms190457.aspx) con valores distintos de NULL en todas las tablas de gran tamaño. Sin índices agrupados, la exportación podría no producirse si tarda más de 6-12 horas. Esto es porque el servicio de exportación de hello necesita toocomplete una tabla tabla examen tootry tooexport todo. Una buena manera toodetermine si las tablas están optimizadas para la exportación es toorun **DBCC SHOW_STATISTICS** y asegúrese de que ese hello *RANGE_HI_KEY* no es null y su valor tiene distribución óptimas. Para obtener más información, consulte [DBCC SHOW_STATISTICS](https://msdn.microsoft.com/library/ms174384.aspx).

> [!NOTE]
> Bacpac no está previsto toobe utilizado para las operaciones de copia de seguridad y restauración. Azure SQL Database crea automáticamente copias de seguridad para cada base de datos de usuario. Para detalles, consulte [Información general sobre la continuidad empresarial](sql-database-business-continuity.md) y [Copias de seguridad de SQL Database](sql-database-automated-backups.md).  
> 

## <a name="export-tooa-bacpac-file-using-hello-azure-portal"></a>Exportar archivo BACPAC de tooa mediante Hola portal de Azure

Hola tooexport una base de datos mediante [portal de Azure](https://portal.azure.com), abra la página de hello para la base de datos y haga clic en **exportar** en la barra de herramientas de Hola. Especificar nombre de archivo BACPAC de Hola, proporcione la cuenta de almacenamiento de Azure de Hola y el contenedor para la exportación de Hola y proporcionan la base de datos de origen de toohello de tooconnect de hello las credenciales.  

![Exportación de base de datos](./media/sql-database-export/database-export.png)

progreso de hello toomonitor de hello en operación de exportación, Abrir página Hola Hola servidor lógico que contiene Hola base de datos que se va a exportar. Desplácese hacia abajo demasiado**Operations** y, a continuación, haga clic en **importación/exportación** historial.

![exportar historial](./media/sql-database-export/export-history.png)
![exportar el estado del historial](./media/sql-database-export/export-history2.png)

## <a name="export-tooa-bacpac-file-using-hello-sqlpackage-utility"></a>Exportar archivo BACPAC de tooa con hello SQLPackage utilidad

tooexport una instancia de SQL de base de datos utilizando hello [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) utilidad de línea de comandos, consulte [exportar parámetros y propiedades](https://msdn.microsoft.com/library/hh550080.aspx#Export Parameters and Properties). Hola SQLPackage utilidad se suministra con versiones más recientes de Hola de [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) y [SQL Server Data Tools para Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), o bien puede descargar la versión más reciente de Hola de [ SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) directamente desde Microsoft hello centro de descarga.

Te recomendamos que uses Hola de hello SQLPackage utilidad para escalabilidad y rendimiento en la mayoría de los entornos de producción. Para un equipo de asesoramiento de cliente de SQL Server utilizando los archivos BACPAC, consulte el blog sobre la migración [migración desde SQL Server tooAzure base de datos de SQL mediante archivos BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).

Este ejemplo se muestra cómo tooexport una base de datos con SqlPackage.exe Universal autenticación de Active Directory:

```cmd
SqlPackage.exe /a:Export /tf:testExport.bacpac /scs:"Data Source=apptestserver.database.windows.net;Initial Catalog=MyDB;" /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="export-tooa-bacpac-file-using-sql-server-management-studio-ssms"></a>Exportar archivo BACPAC de tooa mediante SQL Server Management Studio (SSMS)

las versiones más recientes de Hola de SQL Server Management Studio también proporcionan un tooexport Asistente para un archivo BACPAC de tooa de base de datos de SQL Azure. Vea hello [exportar una aplicación de capa de datos](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application).

## <a name="export-tooa-bacpac-file-using-powershell"></a>Exportar archivo BACPAC de tooa con PowerShell

Hola de uso [AzureRmSqlDatabaseExport New](/powershell/module/azurerm.sql/new-azurermsqldatabaseexport) cmdlet toosubmit un toohello de solicitud de base de datos de exportación de servicio de base de datos de SQL Azure. Según el tamaño de saludo de la base de datos, la operación de exportación Hola puede tardar algunos toocomplete de tiempo.

 ```powershell
 $exportRequest = New-AzureRmSqlDatabaseExport -ResourceGroupName $ResourceGroupName -ServerName $ServerName `
   -DatabaseName $DatabaseName -StorageKeytype $StorageKeytype -StorageKey $StorageKey -StorageUri $BacpacUri `
   -AdministratorLogin $creds.UserName -AdministratorLoginPassword $creds.Password
 ```

estado de hello toocheck de hello solicitud de exportación, use hello [AzureRmSqlDatabaseImportExportStatus Get](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet. Si se ejecuta inmediatamente después de hello solicitud normalmente devuelve **estado: InProgress**. Cuando vea **estado: se realizó correctamente** Hola exportar.

```powershell
$exportStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $exportRequest.OperationStatusLink
[Console]::Write("Exporting")
while ($exportStatus.Status -eq "InProgress")
{
    $exportStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $exportRequest.OperationStatusLink
    [Console]::Write(".")
    Start-Sleep -s 10
}
[Console]::WriteLine("")
$exportStatus
```

## <a name="next-steps"></a>Pasos siguientes

* toolearn acerca de la retención de copia de seguridad a largo plazo de una copia de seguridad de base de datos de SQL Azure como una alternativa tooexported una base de datos con fines de archivo, consulte [retención de copia de seguridad a largo plazo](sql-database-long-term-retention.md).
- Para un equipo de asesoramiento de cliente de SQL Server utilizando los archivos BACPAC, consulte el blog sobre la migración [migración desde SQL Server tooAzure base de datos de SQL mediante archivos BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).
* vea toolearn acerca de cómo importar una base de datos de SQL Server de tooa BACPAC, [importar una base de datos de SQL Server de tooa BACPCAC](https://msdn.microsoft.com/library/hh710052.aspx).
* toolearn acerca de cómo exportar un BACPAC desde una base de datos de SQL Server, vea [exportar una aplicación de capa de datos](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application) y [migrar la base de datos primer](sql-database-migrate-your-sql-server-database.md).
* Si va a exportar desde SQL Server como un tooAzure de toomigration preludio base de datos SQL, consulte [migrar un tooAzure de base de datos base de datos SQL de SQL Server](sql-database-cloud-migrate.md).
