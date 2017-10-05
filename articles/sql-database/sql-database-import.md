---
title: "Importación de un archivo BACPAC para crear una base de datos de Azure SQL | Microsoft Docs"
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
ms.openlocfilehash: 285e17ed6d0ce700cb518864df7a3b5f5e55bee5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="import-a-bacpac-file-to-a-new-azure-sql-database"></a><span data-ttu-id="9304d-103">Importación de un archivo BACPAC en una base de datos de Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="9304d-103">Import a BACPAC file to a new Azure SQL Database</span></span>

<span data-ttu-id="9304d-104">Cuando sea preciso importar una base de datos de un archivo o al realizar una migración desde otra plataforma, el esquema y los datos de la base de datos y los datos se pueden importar desde un archivo [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4).</span><span class="sxs-lookup"><span data-stu-id="9304d-104">When you need to import a database from an archive or when migrating from another platform, you can import the database schema and data from a [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) file.</span></span> <span data-ttu-id="9304d-105">Un archivo BACPAC es un archivo ZIP con una extensión de BACPAC que contiene los metadatos y los datos de una base de datos de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9304d-105">A BACPAC file is a ZIP file with an extension of BACPAC containing the metadata and data from a SQL Server database.</span></span> <span data-ttu-id="9304d-106">Los archivos BACPAC se pueden importar de Azure Blob Storage (solo almacenamiento estándar) o del almacenamiento local en una ubicación local.</span><span class="sxs-lookup"><span data-stu-id="9304d-106">A BACPAC file can be imported from Azure blob storage (standard storage only) or from local storage in an on-premises location.</span></span> <span data-ttu-id="9304d-107">Para maximizar la velocidad de importación, es aconsejable especificar un nivel de rendimiento y una capa de servicio superiores, como un P6 y, después escalarlos hacia abajo tanto como sea apropiado cuando la importación se haya realizado correctamente.</span><span class="sxs-lookup"><span data-stu-id="9304d-107">To maximize the import speed, we recommend that you specify a higher service tier and performance level, such as a P6, and then scale to down as appropriate after the import is successful.</span></span> <span data-ttu-id="9304d-108">Además, el nivel de compatibilidad de la base de datos después de la importación se basa en el nivel de compatibilidad de la base de datos de origen.</span><span class="sxs-lookup"><span data-stu-id="9304d-108">Also, the database compatibility level after the import is based on the compatibility level of the source database.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="9304d-109">Después de migrar la base de datos a Azure SQL Database, puede elegir utilizar la base de datos en su nivel de compatibilidad actual (nivel 100 para la base de datos AdventureWorks2008R2) o en un nivel superior.</span><span class="sxs-lookup"><span data-stu-id="9304d-109">After you migrate your database to Azure SQL Database, you can choose to operate the database at its current compatibility level (level 100 for the AdventureWorks2008R2 database) or at a higher level.</span></span> <span data-ttu-id="9304d-110">Para más información acerca de las implicaciones y las opciones para la utilización de una base de datos en un nivel de compatibilidad específico, consulte [ALTER DATABASE (Transact-SQL) Compatibility Level](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level) [Nivel de compatibilidad de ALTER DATABASE (Transact-SQL)].</span><span class="sxs-lookup"><span data-stu-id="9304d-110">For more information on the implications and options for operating a database at a specific compatibility level, see [ALTER DATABASE Compatibility Level](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).</span></span> <span data-ttu-id="9304d-111">Vea también [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) para obtener información sobre los valores de nivel de base de datos adicionales relacionados con los niveles de compatibilidad.</span><span class="sxs-lookup"><span data-stu-id="9304d-111">See also [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) for information about additional database-level settings related to compatibility levels.</span></span>   >

> [!NOTE]
> <span data-ttu-id="9304d-112">Para importar un archivo BACPAC en una base de datos nueva, primero es preciso crear un servidor lógico de Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="9304d-112">To import a BACPAC to a new database, you must first create an Azure SQL Database logical server.</span></span> <span data-ttu-id="9304d-113">Para obtener un tutorial que le muestre cómo migrar una base de datos de SQL Server a Azure SQL Database mediante SQLPackage, consulte [Migrate your SQL Server database to Azure SQL Database](sql-database-migrate-your-sql-server-database.md) (Migración de una base de datos de SQL Server a Azure SQL Database)</span><span class="sxs-lookup"><span data-stu-id="9304d-113">For a tutorial showing you how to migrate a SQL Server database to Azure SQL Database using SQLPackage, see [Migrate a SQL Server Database](sql-database-migrate-your-sql-server-database.md)</span></span>
>

## <a name="import-from-a-bacpac-file-using-azure-portal"></a><span data-ttu-id="9304d-114">Importación de un archivo BACPAC mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9304d-114">Import from a BACPAC file using Azure portal</span></span>

<span data-ttu-id="9304d-115">En este artículo encontrará instrucciones para crear una base de datos de Azure SQL Database a partir de un archivo BACPAC almacenado en Azure Blob Storage mediante [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9304d-115">This article provides directions for creating an Azure SQL database from a BACPAC file stored in Azure blob storage using the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="9304d-116">La importación mediante Azure Portal solo admite la importación de un archivo BACPAC desde Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="9304d-116">Import using the Azure portal only supports importing a BACPAC file from Azure blob storage.</span></span>

<span data-ttu-id="9304d-117">Para importar una base de datos mediante Azure Portal, abra la página de la base de datos y haga clic en **Importar** en la barra de herramientas.</span><span class="sxs-lookup"><span data-stu-id="9304d-117">To import a database using the Azure portal, open the page for your database and click **Import** on the toolbar.</span></span> <span data-ttu-id="9304d-118">Especifique la cuenta de almacenamiento y el contenedor, y seleccione el archivo BACPAC que desea importar.</span><span class="sxs-lookup"><span data-stu-id="9304d-118">Specify the storage account and container, and select the BACPAC file you want to import.</span></span> <span data-ttu-id="9304d-119">Seleccione el tamaño de la nueva base de datos (normalmente el mismo que el origen) y proporcione las credenciales del servidor SQL Server de destino.</span><span class="sxs-lookup"><span data-stu-id="9304d-119">Select the size of the new database (usually the same as origin) and provide the destination SQL Server credentials.</span></span>  

   ![Importación de base de datos](./media/sql-database-import/import.png)

<span data-ttu-id="9304d-121">Para supervisar el progreso de la operación de importación, abra la página del servidor lógico que contiene la base de datos que se va a importar.</span><span class="sxs-lookup"><span data-stu-id="9304d-121">To monitor the progress of the import operation, open the page for the logical server containing the database being imported.</span></span> <span data-ttu-id="9304d-122">Desplácese hacia abajo hasta **Operaciones** y, después, haga clic en el historial de **importación y exportación**.</span><span class="sxs-lookup"><span data-stu-id="9304d-122">Scroll down to **Operations** and then click **Import/Export** history.</span></span>

### <a name="monitor-the-progress-of-an-import-operation"></a><span data-ttu-id="9304d-123">Supervisión del progreso de la operación de importación</span><span class="sxs-lookup"><span data-stu-id="9304d-123">Monitor the progress of an import operation</span></span>

<span data-ttu-id="9304d-124">Para supervisar el progreso de la operación de importación, abra la página del servidor lógico a la que se va a la importar base de datos.</span><span class="sxs-lookup"><span data-stu-id="9304d-124">To monitor the progress of the import operation, open the page for the logical server into which the database is being imported imported.</span></span> <span data-ttu-id="9304d-125">Desplácese hacia abajo hasta **Operaciones** y, después, haga clic en el historial de **importación y exportación**.</span><span class="sxs-lookup"><span data-stu-id="9304d-125">Scroll down to **Operations** and then click **Import/Export** history.</span></span>
   
   <span data-ttu-id="9304d-126">![importar](./media/sql-database-import/import-history.png) ![estado de la importación](./media/sql-database-import/import-status.png)</span><span class="sxs-lookup"><span data-stu-id="9304d-126">![import](./media/sql-database-import/import-history.png) ![import status](./media/sql-database-import/import-status.png)</span></span>

<span data-ttu-id="9304d-127">Para comprobar que la base de datos está activa en el servidor, haga clic en **Bases de datos SQL** y compruebe que la nueva base de datos esté **En línea**.</span><span class="sxs-lookup"><span data-stu-id="9304d-127">To verify the database is live on the server, click **SQL databases** and verify the new database is **Online**.</span></span>

## <a name="import-from-a-bacpac-file-using-sqlpackage"></a><span data-ttu-id="9304d-128">Importación de un archivo BACPAC mediante SQLPackage</span><span class="sxs-lookup"><span data-stu-id="9304d-128">Import from a BACPAC file using SQLPackage</span></span>

<span data-ttu-id="9304d-129">Para importar una base de datos SQL mediante la utilidad de línea de comandos [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx), consulte [Parámetros y propiedades de la importación](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties).</span><span class="sxs-lookup"><span data-stu-id="9304d-129">To import a SQL database using the [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) command-line utility, see [Import parameters and properties](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties).</span></span> <span data-ttu-id="9304d-130">La utilidad SQLPackage incluye las versiones más recientes de [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) y [SQL Server Data Tools para Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), o bien puede descargar la versión más reciente de [SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) directamente desde el Centro de descarga de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9304d-130">The SQLPackage utility ships with the latest versions of [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) and [SQL Server Data Tools for Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), or you can download the latest version of [SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) directly from the Microsoft download center.</span></span>

<span data-ttu-id="9304d-131">Se recomienda usar la utilidad SQLPackage para la escala y el rendimiento en la mayoría de los entornos de producción.</span><span class="sxs-lookup"><span data-stu-id="9304d-131">We recommend the use of the SQLPackage utility for scale and performance in most production environments.</span></span> <span data-ttu-id="9304d-132">Consulte cómo [migrar de SQL Server a Azure SQL Database con archivos BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/) en el blog de Customer Advisory Team de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9304d-132">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server to Azure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>

<span data-ttu-id="9304d-133">Consulte el siguiente comando SQLPackage para ver un script de ejemplo para importar la base de datos **AdventureWorks2008R2** desde el almacenamiento local a un servidor lógico de Azure SQL Database, que en este ejemplo se llama **mynewserver20170403**.</span><span class="sxs-lookup"><span data-stu-id="9304d-133">See the following SQLPackage command for a script example for how to import the **AdventureWorks2008R2** database from local storage to an Azure SQL Database logical server, called **mynewserver20170403** in this example.</span></span> <span data-ttu-id="9304d-134">Este script muestra la creación de una base de datos nueva denominada **myMigratedDatabase**, con una capa de servicio de **Premium** y un objetivo de servicio de **P6**.</span><span class="sxs-lookup"><span data-stu-id="9304d-134">This script shows the creation of a new database called **myMigratedDatabase**, with a service tier of **Premium**, and a Service Objective of **P6**.</span></span> <span data-ttu-id="9304d-135">Cambie estos valores según sea apropiado para su entorno.</span><span class="sxs-lookup"><span data-stu-id="9304d-135">Change these values as appropriate to your environment.</span></span>

```cmd
SqlPackage.exe /a:import /tcs:"Data Source=mynewserver20170403.database.windows.net;Initial Catalog=myMigratedDatabase;User Id=ServerAdmin;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
```

   ![importación de sqlpackage](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> <span data-ttu-id="9304d-137">Un servidor lógico de Azure SQL Database escucha en el puerto 1433.</span><span class="sxs-lookup"><span data-stu-id="9304d-137">An Azure SQL Database logical server listens on port 1433.</span></span> <span data-ttu-id="9304d-138">Si intenta conectarse a un servidor lógico de Azure SQL Database desde dentro de un firewall corporativo, este puerto debe estar abierto en el firewall corporativo para poder conectarse correctamente.</span><span class="sxs-lookup"><span data-stu-id="9304d-138">If you are attempting to connect to an Azure SQL Database logical server from within a corporate firewall, this port must be open in the corporate firewall for you to successfully connect.</span></span>
>

<span data-ttu-id="9304d-139">Este ejemplo muestra cómo importar una base de datos con SqlPackage.exe con Autenticación universal de Active Directory:</span><span class="sxs-lookup"><span data-stu-id="9304d-139">This example shows how to import a database using SqlPackage.exe with Active Directory Universal Authentication:</span></span>

```cmd
SqlPackage.exe /a:Import /sf:testExport.bacpac /tdn:NewDacFX /tsn:apptestserver.database.windows.net /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="import-from-a-bacpac-file-using-powershell"></a><span data-ttu-id="9304d-140">Importación de un archivo BACPAC mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="9304d-140">Import from a BACPAC file using PowerShell</span></span>

<span data-ttu-id="9304d-141">Use el cmdlet [AzureRmSqlDatabaseImport New](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) para enviar una solicitud de importación base de datos al servicio Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="9304d-141">Use the [New-AzureRmSqlDatabaseImport](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) cmdlet to submit an import database request to the Azure SQL Database service.</span></span> <span data-ttu-id="9304d-142">Según el tamaño de su base de datos, la operación de importación puede tardar algún tiempo en completarse.</span><span class="sxs-lookup"><span data-stu-id="9304d-142">Depending on the size of your database, the import operation may take some time to complete.</span></span>

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

<span data-ttu-id="9304d-143">Para comprobar el estado de la solicitud de importación, utilice el cmdlet [AzureRmSqlDatabaseImportExportStatus Get](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus).</span><span class="sxs-lookup"><span data-stu-id="9304d-143">To check the status of the import request, use the [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet.</span></span> <span data-ttu-id="9304d-144">Si se ejecuta inmediatamente después de la solicitud, normalmente devuelve **Status: InProgress**.</span><span class="sxs-lookup"><span data-stu-id="9304d-144">Running this immediately after the request usually returns **Status: InProgress**.</span></span> <span data-ttu-id="9304d-145">Cuando vea **Status: Succeeded**, la importación se habrá completado.</span><span class="sxs-lookup"><span data-stu-id="9304d-145">When you see **Status: Succeeded** the import is complete.</span></span>

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
<span data-ttu-id="9304d-146">Para ver otro ejemplo de script, consulte [Importación de una base de datos desde un archivo BACPAC](scripts/sql-database-import-from-bacpac-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="9304d-146">For another script example, see [Import a database from a BACPAC file](scripts/sql-database-import-from-bacpac-powershell.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9304d-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9304d-147">Next steps</span></span>
* <span data-ttu-id="9304d-148">Para aprender a conectarse a una base de datos de SQL Database importada y realizar consultas en ella, consulte [Conexión a SQL Database con SQL Server Management Studio y ejecución de una consulta T-SQL de ejemplo](sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="9304d-148">To learn how to connect to and query an imported SQL Database, see [Connect to SQL Database with SQL Server Management Studio and perform a sample T-SQL query](sql-database-connect-query-ssms.md).</span></span>
* <span data-ttu-id="9304d-149">Consulte cómo [migrar de SQL Server a Azure SQL Database con archivos BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/) en el blog de Customer Advisory Team de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9304d-149">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server to Azure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>
* <span data-ttu-id="9304d-150">Para obtener información sobre el proceso de migración de bases de datos de SQL Server completo, incluidas las recomendaciones de rendimiento, consulte [Migración de una base de datos de SQL Server a Azure SQL Database](sql-database-cloud-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="9304d-150">For a discussion of the entire SQL Server database migration process, including performance recommendations, see [Migrate a SQL Server database to Azure SQL Database](sql-database-cloud-migrate.md).</span></span>



