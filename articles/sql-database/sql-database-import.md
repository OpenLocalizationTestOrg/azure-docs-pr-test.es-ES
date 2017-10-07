---
title: aaaImport un BACPAC de archivos toocreate una base de datos SQL de Azure | Documentos de Microsoft
description: "Cree una base de datos de Azure SQL Database nueva mediante la importación de archivo BACPAC."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: cf9a9631-56aa-4985-a565-1cacc297871d
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.date: 06/26/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 0d5fc93acf27b79502969fcd6199d11161915b19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="import-a-bacpac-file-tooa-new-azure-sql-database"></a>Importar un tooa de archivo BACPAC nueva base de datos de SQL Azure

Cuando necesite tooimport una base de datos desde un archivo o al migrar desde otra plataforma, puede importar esquema de base de datos de Hola y los datos de un [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) archivo. Un archivo BACPAC es un archivo ZIP con una extensión de BACPAC que contiene los metadatos de Hola y los datos de una base de datos de SQL Server. Los archivos BACPAC se pueden importar de Azure Blob Storage (solo almacenamiento estándar) o del almacenamiento local en una ubicación local. velocidad de importación de toomaximize hello, se recomienda que especifique un servicio capa y rendimiento de nivel superior, como un P6 y, a continuación, escalar toodown según corresponda después de importar hello es correcta. Además, nivel de compatibilidad de base de datos de hello después de la importación de Hola se basa en el nivel de compatibilidad de Hola de base de datos de origen de Hola. 

> [!IMPORTANT] 
> Después de migrar la base de datos SQL de tooAzure de base de datos, puede elegir la base de datos de toooperate hello en su nivel de compatibilidad actual (nivel 100 para la base de datos de AdventureWorks2008R2 de hello) o en un nivel superior. Para obtener más información sobre las implicaciones de Hola y opciones para el funcionamiento de una base de datos en un nivel de compatibilidad específico, consulte [nivel de compatibilidad de ALTER DATABASE](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level). Vea también [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) para obtener información acerca de la configuración de nivel de base de datos adicional relacionados con los niveles de toocompatibility.   >

> [!NOTE]
> tooimport BACPAC tooa nueva base de datos, primero debe crear un servidor lógico de la base de datos de SQL Azure. Para obtener un tutorial que muestra cómo toomigrate un SQL Server base de datos tooAzure base de datos SQL mediante SQLPackage, consulte [migrar una base de datos de SQL Server](sql-database-migrate-your-sql-server-database.md)
>

## <a name="import-from-a-bacpac-file-using-azure-portal"></a>Importación de un archivo BACPAC mediante Azure Portal

Este artículo proporciona instrucciones para crear una base de datos de SQL Azure desde un archivo BACPAC almacenado en el almacenamiento de blobs de Azure con hello [portal de Azure](https://portal.azure.com). Una importación mediante Hola portal de Azure solo admite la importación de un archivo BACPAC desde el almacenamiento de blobs de Azure.

tooimport una base de datos mediante Hola portal de Azure, página de hello abierto para la base de datos y haga clic en **importación** en la barra de herramientas de Hola. Especificar cuenta de almacenamiento de Hola y de contenedor y seleccione archivo BACPAC de Hola que quiera tooimport. Seleccione Hola tamaño de base de datos nueva hello (normalmente Hola mismo como origen) y proporcione las credenciales de SQL Server de destino de Hola.  

   ![Importación de base de datos](./media/sql-database-import/import.png)

progreso de hello toomonitor del programa Hola a la operación de importación, Abrir página Hola Hola servidor lógico que contiene Hola base de datos que se va a importar. Desplácese hacia abajo demasiado**Operations** y, a continuación, haga clic en **importación/exportación** historial.

### <a name="monitor-hello-progress-of-an-import-operation"></a>Hola supervisar el progreso de una operación de importación

progreso de hello toomonitor del programa Hola a la operación de importación, Abrir página Hola Hola servidor lógico en qué Hola se va a importar la base de datos importados. Desplácese hacia abajo demasiado**Operations** y, a continuación, haga clic en **importación/exportación** historial.
   
   ![importar](./media/sql-database-import/import-history.png)![estado de la importación](./media/sql-database-import/import-status.png)

base de datos de tooverify hello en vivo en el servidor de hello, haga clic en **bases de datos SQL** y compruebe la base de datos nueva hello es **Online**.

## <a name="import-from-a-bacpac-file-using-sqlpackage"></a>Importación de un archivo BACPAC mediante SQLPackage

tooimport una instancia de SQL de base de datos utilizando hello [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) utilidad de línea de comandos, consulte [importar parámetros y propiedades](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties). Hola SQLPackage utilidad se suministra con versiones más recientes de Hola de [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) y [SQL Server Data Tools para Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), o bien puede descargar la versión más reciente de Hola de [ SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) directamente desde Microsoft hello centro de descarga.

Te recomendamos que uses Hola de hello SQLPackage utilidad para escalabilidad y rendimiento en la mayoría de los entornos de producción. Para un equipo de asesoramiento de cliente de SQL Server utilizando los archivos BACPAC, consulte el blog sobre la migración [migración desde SQL Server tooAzure base de datos de SQL mediante archivos BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).

Vea Hola siguiente comando SQLPackage para obtener un ejemplo de secuencia de comandos para saber cómo hello tooimport **AdventureWorks2008R2** base de datos de almacenamiento local tooan base de datos de SQL Azure servidor lógico, denominado **mynewserver20170403** en este ejemplo. Este script muestra la creación de hello de una base de datos denominada **myMigratedDatabase**, con un nivel de servicio de **Premium**y un objetivo de servicio **P6**. Cambiar estos valores como entorno de tooyour adecuado.

```cmd
SqlPackage.exe /a:import /tcs:"Data Source=mynewserver20170403.database.windows.net;Initial Catalog=myMigratedDatabase;User Id=ServerAdmin;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
```

   ![importación de sqlpackage](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> Un servidor lógico de Azure SQL Database escucha en el puerto 1433. Si estás intentando tooconnect tooan base de datos de SQL Azure servidor lógico desde dentro de un firewall corporativo, este puerto debe estar abierto en el firewall corporativo hello para la conexión se toosuccessfully.
>

Este ejemplo se muestra cómo tooimport una base de datos con SqlPackage.exe Universal autenticación de Active Directory:

```cmd
SqlPackage.exe /a:Import /sf:testExport.bacpac /tdn:NewDacFX /tsn:apptestserver.database.windows.net /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="import-from-a-bacpac-file-using-powershell"></a>Importación de un archivo BACPAC mediante PowerShell

Hola de uso [AzureRmSqlDatabaseImport New](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) cmdlet toosubmit un toohello de solicitud de base de datos de importación servicio de base de datos de SQL Azure. Según el tamaño de saludo de la base de datos, operación de importación de hello puede tardar algunos toocomplete de tiempo.

 ```powershell
 $importRequest = New-AzureRmSqlDatabaseImport -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName "MyImportSample" `
    -DatabaseMaxSizeBytes "262144000" `
    -StorageKeyType "StorageAccessKey" `
    -StorageKey $(Get-AzureRmStorageAccountKey -ResourceGroupName "myResourceGroup" -StorageAccountName $storageaccountname).Value[0] `
    -StorageUri "http://$storageaccountname.blob.core.windows.net/importsample/sample.bacpac" `
    -Edition "Standard" `
    -ServiceObjectiveName "P6" `
    -AdministratorLogin "ServerAdmin" `
    -AdministratorLoginPassword $(ConvertTo-SecureString -String "ASecureP@assw0rd" -AsPlainText -Force)

 ```

estado de hello toocheck del programa Hola a la solicitud de importación, utilice hello [AzureRmSqlDatabaseImportExportStatus Get](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet. Si se ejecuta inmediatamente después de hello solicitud normalmente devuelve **estado: InProgress**. Cuando vea **estado: se realizó correctamente** importación Hola está completa.

```powershell
$importStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $importRequest.OperationStatusLink
[Console]::Write("Importing")
while ($importStatus.Status -eq "InProgress")
{
    $importStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $importRequest.OperationStatusLink
    [Console]::Write(".")
    Start-Sleep -s 10
}
[Console]::WriteLine("")
$importStatus
```

> [!TIP]
Para ver otro ejemplo de script, consulte [Importación de una base de datos desde un archivo BACPAC](scripts/sql-database-import-from-bacpac-powershell.md).

## <a name="next-steps"></a>Pasos siguientes
* toolearn cómo tooconnect tooand consultar una base de datos importados de SQL, consulte [conectarse tooSQL base de datos con SQL Server Management Studio y realizar una consulta de T-SQL de ejemplo](sql-database-connect-query-ssms.md).
* Para un equipo de asesoramiento de cliente de SQL Server utilizando los archivos BACPAC, consulte el blog sobre la migración [migración desde SQL Server tooAzure base de datos de SQL mediante archivos BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).
* Para obtener una explicación Hola todo SQL Server base de datos del proceso de migración, incluidas las recomendaciones de rendimiento, consulte [migrar un tooAzure de base de datos base de datos SQL de SQL Server](sql-database-cloud-migrate.md).



