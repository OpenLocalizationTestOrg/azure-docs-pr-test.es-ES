---
title: aaaRestore una sola tabla de copia de seguridad de base de datos de SQL de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toorestore una sola tabla de copia de seguridad de base de datos de SQL Azure."
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: 340b41bd-9df8-47fb-adfc-03216de38a5e
ms.service: sql-database
ms.custom: business continuity
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: 696d2ac87a70bccdf063bfecb8255723404aa5bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorestore-a-single-table-from-an-azure-sql-database-backup"></a><span data-ttu-id="5a77b-103">Cómo toorestore una sola tabla desde una copia de seguridad de base de datos de SQL Azure</span><span class="sxs-lookup"><span data-stu-id="5a77b-103">How toorestore a single table from an Azure SQL Database backup</span></span>
<span data-ttu-id="5a77b-104">Puede encontrarse con una situación en la que modificar accidentalmente algunos datos en una base de datos SQL y ahora desea toorecover Hola única afectados tabla.</span><span class="sxs-lookup"><span data-stu-id="5a77b-104">You may encounter a situation in which you accidentally modified some data in a SQL database and now you want toorecover hello single affected table.</span></span> <span data-ttu-id="5a77b-105">Este artículo describe cómo toorestore una sola tabla en una base de datos de una base de datos SQL de hello [copias de seguridad automáticas](sql-database-automated-backups.md).</span><span class="sxs-lookup"><span data-stu-id="5a77b-105">This article describes how toorestore a single table in a database from one of hello SQL Database [automatic backups](sql-database-automated-backups.md).</span></span>

## <a name="preparation-steps-rename-hello-table-and-restore-a-copy-of-hello-database"></a><span data-ttu-id="5a77b-106">Pasos de preparación: cambiar el nombre de tabla de Hola y restaure una copia de base de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="5a77b-106">Preparation steps: Rename hello table and restore a copy of hello database</span></span>
1. <span data-ttu-id="5a77b-107">Identificar la tabla de hello en la base de datos de SQL Azure que desea tooreplace con copia de hello restaurado.</span><span class="sxs-lookup"><span data-stu-id="5a77b-107">Identify hello table in your Azure SQL database that you want tooreplace with hello restored copy.</span></span> <span data-ttu-id="5a77b-108">Utilice la tabla de Microsoft SQL Management Studio toorename Hola.</span><span class="sxs-lookup"><span data-stu-id="5a77b-108">Use Microsoft SQL Management Studio toorename hello table.</span></span> <span data-ttu-id="5a77b-109">Por ejemplo, cambiar el nombre de tabla de hello como &lt;nombre de la tabla&gt;_old.</span><span class="sxs-lookup"><span data-stu-id="5a77b-109">For example, rename hello table as &lt;table name&gt;_old.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5a77b-110">tooavoid está bloqueado, asegúrese de que no hay ninguna actividad ejecutar en la tabla de Hola que ha cambiado.</span><span class="sxs-lookup"><span data-stu-id="5a77b-110">tooavoid being blocked, make sure that there's no activity running on hello table that you are renaming.</span></span> <span data-ttu-id="5a77b-111">Si encuentra algún problema, realice este procedimiento durante una ventana de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="5a77b-111">If you encounter issues, make sure that perform this procedure during a maintenance window.</span></span>
   >

2. <span data-ttu-id="5a77b-112">Restaurar una copia de seguridad de su punto de tooa de base de datos en el tiempo que desea que toorecover toousing hello [punto-In_Time restaurar](sql-database-recovery-using-backups.md#point-in-time-restore) pasos.</span><span class="sxs-lookup"><span data-stu-id="5a77b-112">Restore a backup of your database tooa point in time that you want toorecover toousing hello [Point-In_Time Restore](sql-database-recovery-using-backups.md#point-in-time-restore) steps.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5a77b-113">nombre de Hola de base de datos de hello restaurar será en formato de marca de tiempo + DBName Hola; Por ejemplo, **Adventureworks2012_2016-01-01T22-12Z**.</span><span class="sxs-lookup"><span data-stu-id="5a77b-113">hello name of hello restored database will be in hello DBName+TimeStamp format; for example, **Adventureworks2012_2016-01-01T22-12Z**.</span></span> <span data-ttu-id="5a77b-114">Este paso no sobrescribe el nombre de base de datos existente de hello en el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="5a77b-114">This step doesn't overwrite hello existing database name on hello server.</span></span> <span data-ttu-id="5a77b-115">Se trata de una medida de seguridad, y está pensado tooallow se tooverify Hola restaura base de datos antes de quitar la base de datos actual y cambiar el nombre de base de datos de hello restaurar para su uso en producción.</span><span class="sxs-lookup"><span data-stu-id="5a77b-115">This is a safety measure, and it's intended tooallow you tooverify hello restored database before they drop their current database and rename hello restored database for production use.</span></span>
   
## <a name="copying-hello-table-from-hello-restored-database-by-using-hello-sql-database-migration-tool"></a><span data-ttu-id="5a77b-116">Copiando la tabla Hola de hello restaurado la base de datos mediante el uso de la herramienta de migración de base de datos de SQL de Hola</span><span class="sxs-lookup"><span data-stu-id="5a77b-116">Copying hello table from hello restored database by using hello SQL Database Migration tool</span></span>

1. <span data-ttu-id="5a77b-117">Descargue e instale hello [Asistente para migración de base de datos de SQL](https://sqlazuremw.codeplex.com).</span><span class="sxs-lookup"><span data-stu-id="5a77b-117">Download and install hello [SQL Database Migration Wizard](https://sqlazuremw.codeplex.com).</span></span>
2. <span data-ttu-id="5a77b-118">Abra Hola Asistente para migración de base de datos de SQL, en hello **Seleccionar proceso** , seleccione **base de datos en analizar/migrar**y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="5a77b-118">Open hello SQL Database Migration Wizard, on hello **Select Process** page, select **Database under Analyze/Migrate**, and then click **Next**.</span></span>

   ![Asistente para migración de Base de datos SQL: seleccionar proceso](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/1.png)

3. <span data-ttu-id="5a77b-120">Hola **conectar tooServer** diálogo cuadro, aplique Hola después de configuración:</span><span class="sxs-lookup"><span data-stu-id="5a77b-120">In hello **Connect tooServer** dialog box, apply hello following settings:</span></span>

   * <span data-ttu-id="5a77b-121">Nombre del servidor: **su servidor SQL**</span><span class="sxs-lookup"><span data-stu-id="5a77b-121">Server name: **Your SQL server**</span></span>
   * <span data-ttu-id="5a77b-122">Autenticación: **Autenticación de SQL Server**</span><span class="sxs-lookup"><span data-stu-id="5a77b-122">Authentication: **SQL Server Authentication**</span></span>
   * <span data-ttu-id="5a77b-123">Inicio de sesión: **sus datos de inicio de sesión**</span><span class="sxs-lookup"><span data-stu-id="5a77b-123">Login: **Your login**</span></span>
   * <span data-ttu-id="5a77b-124">Contraseña: **su contraseña**</span><span class="sxs-lookup"><span data-stu-id="5a77b-124">Password: **Your password**</span></span>
   * <span data-ttu-id="5a77b-125">**Master DB (List all databases)** [BD maestra (Enumerar todas las bases de datos)]</span><span class="sxs-lookup"><span data-stu-id="5a77b-125">Database: **Master DB (List all databases)**</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5a77b-126">De forma predeterminada el Asistente de hello guarda la información de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="5a77b-126">By default hello wizard saves your login information.</span></span> <span data-ttu-id="5a77b-127">Si no quiere que lo haga, seleccione **Forget Login Information (No recordar la información de inicio de sesión)**.</span><span class="sxs-lookup"><span data-stu-id="5a77b-127">If you don't want it to, select **Forget Login Information**.</span></span>
   >
   
     ![Asistente para migración de base de datos SQL: seleccionar origen, paso 1](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/2.png)
4. <span data-ttu-id="5a77b-129">Hola **Seleccionar origen** cuadro de diálogo, el nombre de la base de datos de hello seleccione Restaurar de hello **pasos de preparación** como origen de la sección y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="5a77b-129">In hello **Select Source** dialog box, select hello restored database name from hello **Preparation steps** section as your source, and then click **Next**.</span></span>
   
    ![Asistente para migración de base de datos SQL: seleccionar origen, paso 2](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/3.png)
5. <span data-ttu-id="5a77b-131">Hola **elegir objetos** cuadro de diálogo, seleccione hello **seleccionar objetos de base de datos específica** opción y, a continuación, seleccione table(or tables) Hola que desea que el servidor de destino de toomigrate toohello.</span><span class="sxs-lookup"><span data-stu-id="5a77b-131">In hello **Choose Objects** dialog box, select hello **Select specific database objects** option, and then select hello table(or tables) that you want toomigrate toohello target server.</span></span>
   <span data-ttu-id="5a77b-132">![Asistente para migración de base de datos SQL: elegir objetos](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)</span><span class="sxs-lookup"><span data-stu-id="5a77b-132">![SQL Database Migration wizard - Choose Objects](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)</span></span>
6. <span data-ttu-id="5a77b-133">En hello **resumen del Asistente para secuencia de comandos** página, haga clic en **Sí** cuando se le pregunta acerca de si está listo toogenerate una secuencia de comandos SQL.</span><span class="sxs-lookup"><span data-stu-id="5a77b-133">On hello **Script Wizard Summary** page, click **Yes** when you’re prompted about whether you’re ready toogenerate a SQL script.</span></span> <span data-ttu-id="5a77b-134">También tiene Hola Hola toosave secuencia de comandos TSQL opción para su uso posterior.</span><span class="sxs-lookup"><span data-stu-id="5a77b-134">You also have hello option toosave hello TSQL Script for later use.</span></span>
   <span data-ttu-id="5a77b-135">![Asistente para migración de base de datos SQL: resumen del Asistente de scripts](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)</span><span class="sxs-lookup"><span data-stu-id="5a77b-135">![SQL Database Migration wizard - Script Wizard Summary](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)</span></span>
7. <span data-ttu-id="5a77b-136">En hello **resumen de los resultados** página, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="5a77b-136">On hello **Results Summary** page, click **Next**.</span></span>
   <span data-ttu-id="5a77b-137">![Asistente para migración de base de datos SQL: resumen de resultados](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)</span><span class="sxs-lookup"><span data-stu-id="5a77b-137">![SQL Database Migration wizard - Results Summary](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)</span></span>
8. <span data-ttu-id="5a77b-138">En hello **configurar conexión de servidor de destino** página, haga clic en **conectar tooServer**y, a continuación, escriba los detalles de hello como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="5a77b-138">On hello **Setup Target Server Connection** page, click **Connect tooServer**, and then enter hello details as follows:</span></span>
   
   * <span data-ttu-id="5a77b-139">**Nombre del servidor**: instancia de servidor de destino</span><span class="sxs-lookup"><span data-stu-id="5a77b-139">**Server Name**: Target server instance</span></span>
   * <span data-ttu-id="5a77b-140">**Autenticación**: **Autenticación de SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="5a77b-140">**Authentication**: **SQL Server authentication**.</span></span> <span data-ttu-id="5a77b-141">Escriba sus credenciales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="5a77b-141">Enter your login credentials.</span></span>
   * <span data-ttu-id="5a77b-142">**Base de datos**: **Master DB (List all databases)** [BD maestra (Enumerar todas las bases de datos)].</span><span class="sxs-lookup"><span data-stu-id="5a77b-142">**Database**: **Master DB (List all databases)**.</span></span> <span data-ttu-id="5a77b-143">Esta opción muestra todas las bases de datos de hello en el servidor de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="5a77b-143">This option lists all hello databases on hello target server.</span></span>
     
     ![Asistente para migración de base de datos SQL: configurar conexión del servidor de destino](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/7.png)
9. <span data-ttu-id="5a77b-145">Haga clic en **conectar**, seleccione la base de datos de destino de Hola que desea toomove Hola tabla y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="5a77b-145">Click **Connect**, select hello target database that you want toomove hello table to, and then click **Next**.</span></span> <span data-ttu-id="5a77b-146">Esto debería termine de ejecutar script de Hola generado previamente y debería ver Hola recién movido la base de datos de destino de toohello copiada de tabla.</span><span class="sxs-lookup"><span data-stu-id="5a77b-146">This should finish running hello previously generated script, and you should see hello newly moved table copied toohello target database.</span></span>

## <a name="verification-step"></a><span data-ttu-id="5a77b-147">Paso de comprobación</span><span class="sxs-lookup"><span data-stu-id="5a77b-147">Verification step</span></span>

- <span data-ttu-id="5a77b-148">Hola de consultas y pruebas recién había copiado tabla toomake seguro de que los datos de hello están intactos.</span><span class="sxs-lookup"><span data-stu-id="5a77b-148">Query and test hello newly copied table toomake sure that hello data is intact.</span></span> <span data-ttu-id="5a77b-149">Tras la confirmación, puede quitar el formulario de hello cambia el nombre de tabla **pasos de preparación** sección.</span><span class="sxs-lookup"><span data-stu-id="5a77b-149">Upon confirmation, you can drop hello renamed table form **Preparation steps** section.</span></span> <span data-ttu-id="5a77b-150">(por ejemplo, &lt;nombre de la tabla&gt;_old).</span><span class="sxs-lookup"><span data-stu-id="5a77b-150">(for example, &lt;table name&gt;_old).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a77b-151">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5a77b-151">Next steps</span></span>
[<span data-ttu-id="5a77b-152">Información general: copias de seguridad automatizadas de Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="5a77b-152">SQL Database automatic backups</span></span>](sql-database-automated-backups.md)

