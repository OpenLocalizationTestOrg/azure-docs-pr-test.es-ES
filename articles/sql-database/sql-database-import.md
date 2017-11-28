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
# <a name="import-a-bacpac-file-tooa-new-azure-sql-database"></a><span data-ttu-id="4cd05-103">Importar un tooa de archivo BACPAC nueva base de datos de SQL Azure</span><span class="sxs-lookup"><span data-stu-id="4cd05-103">Import a BACPAC file tooa new Azure SQL Database</span></span>

<span data-ttu-id="4cd05-104">Cuando necesite tooimport una base de datos desde un archivo o al migrar desde otra plataforma, puede importar esquema de base de datos de Hola y los datos de un [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) archivo.</span><span class="sxs-lookup"><span data-stu-id="4cd05-104">When you need tooimport a database from an archive or when migrating from another platform, you can import hello database schema and data from a [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) file.</span></span> <span data-ttu-id="4cd05-105">Un archivo BACPAC es un archivo ZIP con una extensión de BACPAC que contiene los metadatos de Hola y los datos de una base de datos de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4cd05-105">A BACPAC file is a ZIP file with an extension of BACPAC containing hello metadata and data from a SQL Server database.</span></span> <span data-ttu-id="4cd05-106">Los archivos BACPAC se pueden importar de Azure Blob Storage (solo almacenamiento estándar) o del almacenamiento local en una ubicación local.</span><span class="sxs-lookup"><span data-stu-id="4cd05-106">A BACPAC file can be imported from Azure blob storage (standard storage only) or from local storage in an on-premises location.</span></span> <span data-ttu-id="4cd05-107">velocidad de importación de toomaximize hello, se recomienda que especifique un servicio capa y rendimiento de nivel superior, como un P6 y, a continuación, escalar toodown según corresponda después de importar hello es correcta.</span><span class="sxs-lookup"><span data-stu-id="4cd05-107">toomaximize hello import speed, we recommend that you specify a higher service tier and performance level, such as a P6, and then scale toodown as appropriate after hello import is successful.</span></span> <span data-ttu-id="4cd05-108">Además, nivel de compatibilidad de base de datos de hello después de la importación de Hola se basa en el nivel de compatibilidad de Hola de base de datos de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="4cd05-108">Also, hello database compatibility level after hello import is based on hello compatibility level of hello source database.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="4cd05-109">Después de migrar la base de datos SQL de tooAzure de base de datos, puede elegir la base de datos de toooperate hello en su nivel de compatibilidad actual (nivel 100 para la base de datos de AdventureWorks2008R2 de hello) o en un nivel superior.</span><span class="sxs-lookup"><span data-stu-id="4cd05-109">After you migrate your database tooAzure SQL Database, you can choose toooperate hello database at its current compatibility level (level 100 for hello AdventureWorks2008R2 database) or at a higher level.</span></span> <span data-ttu-id="4cd05-110">Para obtener más información sobre las implicaciones de Hola y opciones para el funcionamiento de una base de datos en un nivel de compatibilidad específico, consulte [nivel de compatibilidad de ALTER DATABASE](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).</span><span class="sxs-lookup"><span data-stu-id="4cd05-110">For more information on hello implications and options for operating a database at a specific compatibility level, see [ALTER DATABASE Compatibility Level](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).</span></span> <span data-ttu-id="4cd05-111">Vea también [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) para obtener información acerca de la configuración de nivel de base de datos adicional relacionados con los niveles de toocompatibility.</span><span class="sxs-lookup"><span data-stu-id="4cd05-111">See also [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) for information about additional database-level settings related toocompatibility levels.</span></span>   >

> [!NOTE]
> <span data-ttu-id="4cd05-112">tooimport BACPAC tooa nueva base de datos, primero debe crear un servidor lógico de la base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="4cd05-112">tooimport a BACPAC tooa new database, you must first create an Azure SQL Database logical server.</span></span> <span data-ttu-id="4cd05-113">Para obtener un tutorial que muestra cómo toomigrate un SQL Server base de datos tooAzure base de datos SQL mediante SQLPackage, consulte [migrar una base de datos de SQL Server](sql-database-migrate-your-sql-server-database.md)</span><span class="sxs-lookup"><span data-stu-id="4cd05-113">For a tutorial showing you how toomigrate a SQL Server database tooAzure SQL Database using SQLPackage, see [Migrate a SQL Server Database](sql-database-migrate-your-sql-server-database.md)</span></span>
>

## <a name="import-from-a-bacpac-file-using-azure-portal"></a><span data-ttu-id="4cd05-114">Importación de un archivo BACPAC mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4cd05-114">Import from a BACPAC file using Azure portal</span></span>

<span data-ttu-id="4cd05-115">Este artículo proporciona instrucciones para crear una base de datos de SQL Azure desde un archivo BACPAC almacenado en el almacenamiento de blobs de Azure con hello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4cd05-115">This article provides directions for creating an Azure SQL database from a BACPAC file stored in Azure blob storage using hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4cd05-116">Una importación mediante Hola portal de Azure solo admite la importación de un archivo BACPAC desde el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="4cd05-116">Import using hello Azure portal only supports importing a BACPAC file from Azure blob storage.</span></span>

<span data-ttu-id="4cd05-117">tooimport una base de datos mediante Hola portal de Azure, página de hello abierto para la base de datos y haga clic en **importación** en la barra de herramientas de Hola.</span><span class="sxs-lookup"><span data-stu-id="4cd05-117">tooimport a database using hello Azure portal, open hello page for your database and click **Import** on hello toolbar.</span></span> <span data-ttu-id="4cd05-118">Especificar cuenta de almacenamiento de Hola y de contenedor y seleccione archivo BACPAC de Hola que quiera tooimport.</span><span class="sxs-lookup"><span data-stu-id="4cd05-118">Specify hello storage account and container, and select hello BACPAC file you want tooimport.</span></span> <span data-ttu-id="4cd05-119">Seleccione Hola tamaño de base de datos nueva hello (normalmente Hola mismo como origen) y proporcione las credenciales de SQL Server de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="4cd05-119">Select hello size of hello new database (usually hello same as origin) and provide hello destination SQL Server credentials.</span></span>  

   ![Importación de base de datos](./media/sql-database-import/import.png)

<span data-ttu-id="4cd05-121">progreso de hello toomonitor del programa Hola a la operación de importación, Abrir página Hola Hola servidor lógico que contiene Hola base de datos que se va a importar.</span><span class="sxs-lookup"><span data-stu-id="4cd05-121">toomonitor hello progress of hello import operation, open hello page for hello logical server containing hello database being imported.</span></span> <span data-ttu-id="4cd05-122">Desplácese hacia abajo demasiado**Operations** y, a continuación, haga clic en **importación/exportación** historial.</span><span class="sxs-lookup"><span data-stu-id="4cd05-122">Scroll down too**Operations** and then click **Import/Export** history.</span></span>

### <a name="monitor-hello-progress-of-an-import-operation"></a><span data-ttu-id="4cd05-123">Hola supervisar el progreso de una operación de importación</span><span class="sxs-lookup"><span data-stu-id="4cd05-123">Monitor hello progress of an import operation</span></span>

<span data-ttu-id="4cd05-124">progreso de hello toomonitor del programa Hola a la operación de importación, Abrir página Hola Hola servidor lógico en qué Hola se va a importar la base de datos importados.</span><span class="sxs-lookup"><span data-stu-id="4cd05-124">toomonitor hello progress of hello import operation, open hello page for hello logical server into which hello database is being imported imported.</span></span> <span data-ttu-id="4cd05-125">Desplácese hacia abajo demasiado**Operations** y, a continuación, haga clic en **importación/exportación** historial.</span><span class="sxs-lookup"><span data-stu-id="4cd05-125">Scroll down too**Operations** and then click **Import/Export** history.</span></span>
   
   <span data-ttu-id="4cd05-126">![importar](./media/sql-database-import/import-history.png)![estado de la importación](./media/sql-database-import/import-status.png)</span><span class="sxs-lookup"><span data-stu-id="4cd05-126">![import](./media/sql-database-import/import-history.png) ![import status](./media/sql-database-import/import-status.png)</span></span>

<span data-ttu-id="4cd05-127">base de datos de tooverify hello en vivo en el servidor de hello, haga clic en **bases de datos SQL** y compruebe la base de datos nueva hello es **Online**.</span><span class="sxs-lookup"><span data-stu-id="4cd05-127">tooverify hello database is live on hello server, click **SQL databases** and verify hello new database is **Online**.</span></span>

## <a name="import-from-a-bacpac-file-using-sqlpackage"></a><span data-ttu-id="4cd05-128">Importación de un archivo BACPAC mediante SQLPackage</span><span class="sxs-lookup"><span data-stu-id="4cd05-128">Import from a BACPAC file using SQLPackage</span></span>

<span data-ttu-id="4cd05-129">tooimport una instancia de SQL de base de datos utilizando hello [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) utilidad de línea de comandos, consulte [importar parámetros y propiedades](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties).</span><span class="sxs-lookup"><span data-stu-id="4cd05-129">tooimport a SQL database using hello [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) command-line utility, see [Import parameters and properties](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties).</span></span> <span data-ttu-id="4cd05-130">Hola SQLPackage utilidad se suministra con versiones más recientes de Hola de [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) y [SQL Server Data Tools para Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), o bien puede descargar la versión más reciente de Hola de [ SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) directamente desde Microsoft hello centro de descarga.</span><span class="sxs-lookup"><span data-stu-id="4cd05-130">hello SQLPackage utility ships with hello latest versions of [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) and [SQL Server Data Tools for Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), or you can download hello latest version of [SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) directly from hello Microsoft download center.</span></span>

<span data-ttu-id="4cd05-131">Te recomendamos que uses Hola de hello SQLPackage utilidad para escalabilidad y rendimiento en la mayoría de los entornos de producción.</span><span class="sxs-lookup"><span data-stu-id="4cd05-131">We recommend hello use of hello SQLPackage utility for scale and performance in most production environments.</span></span> <span data-ttu-id="4cd05-132">Para un equipo de asesoramiento de cliente de SQL Server utilizando los archivos BACPAC, consulte el blog sobre la migración [migración desde SQL Server tooAzure base de datos de SQL mediante archivos BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span><span class="sxs-lookup"><span data-stu-id="4cd05-132">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server tooAzure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>

<span data-ttu-id="4cd05-133">Vea Hola siguiente comando SQLPackage para obtener un ejemplo de secuencia de comandos para saber cómo hello tooimport **AdventureWorks2008R2** base de datos de almacenamiento local tooan base de datos de SQL Azure servidor lógico, denominado **mynewserver20170403** en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="4cd05-133">See hello following SQLPackage command for a script example for how tooimport hello **AdventureWorks2008R2** database from local storage tooan Azure SQL Database logical server, called **mynewserver20170403** in this example.</span></span> <span data-ttu-id="4cd05-134">Este script muestra la creación de hello de una base de datos denominada **myMigratedDatabase**, con un nivel de servicio de **Premium**y un objetivo de servicio **P6**.</span><span class="sxs-lookup"><span data-stu-id="4cd05-134">This script shows hello creation of a new database called **myMigratedDatabase**, with a service tier of **Premium**, and a Service Objective of **P6**.</span></span> <span data-ttu-id="4cd05-135">Cambiar estos valores como entorno de tooyour adecuado.</span><span class="sxs-lookup"><span data-stu-id="4cd05-135">Change these values as appropriate tooyour environment.</span></span>

```cmd
SqlPackage.exe /a:import /tcs:"Data Source=mynewserver20170403.database.windows.net;Initial Catalog=myMigratedDatabase;User Id=ServerAdmin;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
```

   ![importación de sqlpackage](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> <span data-ttu-id="4cd05-137">Un servidor lógico de Azure SQL Database escucha en el puerto 1433.</span><span class="sxs-lookup"><span data-stu-id="4cd05-137">An Azure SQL Database logical server listens on port 1433.</span></span> <span data-ttu-id="4cd05-138">Si estás intentando tooconnect tooan base de datos de SQL Azure servidor lógico desde dentro de un firewall corporativo, este puerto debe estar abierto en el firewall corporativo hello para la conexión se toosuccessfully.</span><span class="sxs-lookup"><span data-stu-id="4cd05-138">If you are attempting tooconnect tooan Azure SQL Database logical server from within a corporate firewall, this port must be open in hello corporate firewall for you toosuccessfully connect.</span></span>
>

<span data-ttu-id="4cd05-139">Este ejemplo se muestra cómo tooimport una base de datos con SqlPackage.exe Universal autenticación de Active Directory:</span><span class="sxs-lookup"><span data-stu-id="4cd05-139">This example shows how tooimport a database using SqlPackage.exe with Active Directory Universal Authentication:</span></span>

```cmd
SqlPackage.exe /a:Import /sf:testExport.bacpac /tdn:NewDacFX /tsn:apptestserver.database.windows.net /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="import-from-a-bacpac-file-using-powershell"></a><span data-ttu-id="4cd05-140">Importación de un archivo BACPAC mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="4cd05-140">Import from a BACPAC file using PowerShell</span></span>

<span data-ttu-id="4cd05-141">Hola de uso [AzureRmSqlDatabaseImport New](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) cmdlet toosubmit un toohello de solicitud de base de datos de importación servicio de base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="4cd05-141">Use hello [New-AzureRmSqlDatabaseImport](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) cmdlet toosubmit an import database request toohello Azure SQL Database service.</span></span> <span data-ttu-id="4cd05-142">Según el tamaño de saludo de la base de datos, operación de importación de hello puede tardar algunos toocomplete de tiempo.</span><span class="sxs-lookup"><span data-stu-id="4cd05-142">Depending on hello size of your database, hello import operation may take some time toocomplete.</span></span>

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

<span data-ttu-id="4cd05-143">estado de hello toocheck del programa Hola a la solicitud de importación, utilice hello [AzureRmSqlDatabaseImportExportStatus Get](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4cd05-143">toocheck hello status of hello import request, use hello [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet.</span></span> <span data-ttu-id="4cd05-144">Si se ejecuta inmediatamente después de hello solicitud normalmente devuelve **estado: InProgress**.</span><span class="sxs-lookup"><span data-stu-id="4cd05-144">Running this immediately after hello request usually returns **Status: InProgress**.</span></span> <span data-ttu-id="4cd05-145">Cuando vea **estado: se realizó correctamente** importación Hola está completa.</span><span class="sxs-lookup"><span data-stu-id="4cd05-145">When you see **Status: Succeeded** hello import is complete.</span></span>

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
<span data-ttu-id="4cd05-146">Para ver otro ejemplo de script, consulte [Importación de una base de datos desde un archivo BACPAC](scripts/sql-database-import-from-bacpac-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="4cd05-146">For another script example, see [Import a database from a BACPAC file](scripts/sql-database-import-from-bacpac-powershell.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4cd05-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4cd05-147">Next steps</span></span>
* <span data-ttu-id="4cd05-148">toolearn cómo tooconnect tooand consultar una base de datos importados de SQL, consulte [conectarse tooSQL base de datos con SQL Server Management Studio y realizar una consulta de T-SQL de ejemplo](sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="4cd05-148">toolearn how tooconnect tooand query an imported SQL Database, see [Connect tooSQL Database with SQL Server Management Studio and perform a sample T-SQL query](sql-database-connect-query-ssms.md).</span></span>
* <span data-ttu-id="4cd05-149">Para un equipo de asesoramiento de cliente de SQL Server utilizando los archivos BACPAC, consulte el blog sobre la migración [migración desde SQL Server tooAzure base de datos de SQL mediante archivos BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span><span class="sxs-lookup"><span data-stu-id="4cd05-149">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server tooAzure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>
* <span data-ttu-id="4cd05-150">Para obtener una explicación Hola todo SQL Server base de datos del proceso de migración, incluidas las recomendaciones de rendimiento, consulte [migrar un tooAzure de base de datos base de datos SQL de SQL Server](sql-database-cloud-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="4cd05-150">For a discussion of hello entire SQL Server database migration process, including performance recommendations, see [Migrate a SQL Server database tooAzure SQL Database](sql-database-cloud-migrate.md).</span></span>



