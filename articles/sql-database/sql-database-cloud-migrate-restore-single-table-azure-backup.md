---
title: "Restaurar una única tabla de la copia de seguridad de Azure SQL Database | Microsoft Docs"
description: "Obtenga información sobre cómo restaurar una única tabla de la copia de seguridad de Base de datos SQL de Azure."
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
ms.openlocfilehash: 8c750c503d10ea63b9665958b96db2dfea3d9a3c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-restore-a-single-table-from-an-azure-sql-database-backup"></a><span data-ttu-id="0cfe4-103">Restauración de una única tabla a partir de una copia de seguridad de Base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="0cfe4-103">How to restore a single table from an Azure SQL Database backup</span></span>
<span data-ttu-id="0cfe4-104">Puede pasarle que haya modificado algunos datos por error en una base de datos SQL y ahora desee recuperar la única tabla afectada.</span><span class="sxs-lookup"><span data-stu-id="0cfe4-104">You may encounter a situation in which you accidentally modified some data in a SQL database and now you want to recover the single affected table.</span></span> <span data-ttu-id="0cfe4-105">En este artículo se describe cómo restaurar una única tabla de una base de datos desde una de las [copias de seguridad automáticas](sql-database-automated-backups.md)de Base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="0cfe4-105">This article describes how to restore a single table in a database from one of the SQL Database [automatic backups](sql-database-automated-backups.md).</span></span>

## <a name="preparation-steps-rename-the-table-and-restore-a-copy-of-the-database"></a><span data-ttu-id="0cfe4-106">Pasos de preparación: cambiar el nombre de la tabla y restaurar una copia de la base de datos</span><span class="sxs-lookup"><span data-stu-id="0cfe4-106">Preparation steps: Rename the table and restore a copy of the database</span></span>
1. <span data-ttu-id="0cfe4-107">Identifique la tabla en la base de datos SQL de Azure que desee reemplazar por la copia restaurada.</span><span class="sxs-lookup"><span data-stu-id="0cfe4-107">Identify the table in your Azure SQL database that you want to replace with the restored copy.</span></span> <span data-ttu-id="0cfe4-108">Use Microsoft SQL Management Studio para cambiar el nombre de la tabla.</span><span class="sxs-lookup"><span data-stu-id="0cfe4-108">Use Microsoft SQL Management Studio to rename the table.</span></span> <span data-ttu-id="0cfe4-109">Por ejemplo, cambie el nombre de la tabla como &lt;nombre de la tabla&gt;_old.</span><span class="sxs-lookup"><span data-stu-id="0cfe4-109">For example, rename the table as &lt;table name&gt;_old.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0cfe4-110">Para evitar que se bloquee, asegúrese de que no haya ninguna actividad ejecutándose en la tabla a la que le está cambiando el nombre.</span><span class="sxs-lookup"><span data-stu-id="0cfe4-110">To avoid being blocked, make sure that there's no activity running on the table that you are renaming.</span></span> <span data-ttu-id="0cfe4-111">Si encuentra algún problema, realice este procedimiento durante una ventana de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="0cfe4-111">If you encounter issues, make sure that perform this procedure during a maintenance window.</span></span>
   >

2. <span data-ttu-id="0cfe4-112">Restaure una copia de seguridad de su base de datos al punto temporal que desee recuperar; para ello, siga los pasos descritos en [Restauración a un momento dado](sql-database-recovery-using-backups.md#point-in-time-restore).</span><span class="sxs-lookup"><span data-stu-id="0cfe4-112">Restore a backup of your database to a point in time that you want to recover to using the [Point-In_Time Restore](sql-database-recovery-using-backups.md#point-in-time-restore) steps.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0cfe4-113">El nombre de la base de datos restaurada tendrá el formato nombreBaseDeDatos+MarcaDeTiempo; por ejemplo, **AdventureWorks2012_2016-01-01T22-12Z**.</span><span class="sxs-lookup"><span data-stu-id="0cfe4-113">The name of the restored database will be in the DBName+TimeStamp format; for example, **Adventureworks2012_2016-01-01T22-12Z**.</span></span> <span data-ttu-id="0cfe4-114">Con este paso no se sobrescribe el nombre de la base de datos existente en el servidor.</span><span class="sxs-lookup"><span data-stu-id="0cfe4-114">This step doesn't overwrite the existing database name on the server.</span></span> <span data-ttu-id="0cfe4-115">Se trata de una medida de seguridad, diseñada para permitirle comprobar la base de datos restaurada antes de deshacerse de su base de datos actual y cambiar el nombre de la base de datos restaurada para su uso en producción.</span><span class="sxs-lookup"><span data-stu-id="0cfe4-115">This is a safety measure, and it's intended to allow you to verify the restored database before they drop their current database and rename the restored database for production use.</span></span>
   
## <a name="copying-the-table-from-the-restored-database-by-using-the-sql-database-migration-tool"></a><span data-ttu-id="0cfe4-116">Copiar la tabla de la base de datos restaurada mediante la herramienta de migración de Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="0cfe4-116">Copying the table from the restored database by using the SQL Database Migration tool</span></span>

1. <span data-ttu-id="0cfe4-117">Descargue e instale el [Asistente para migración de Base de datos SQL](https://sqlazuremw.codeplex.com).</span><span class="sxs-lookup"><span data-stu-id="0cfe4-117">Download and install the [SQL Database Migration Wizard](https://sqlazuremw.codeplex.com).</span></span>
2. <span data-ttu-id="0cfe4-118">Abra el Asistente para migración de SQL Database; en la página **Select Process** (Seleccionar proceso), seleccione **Base de datos en la sección Analyze/Migrate** (Analizar o migrar) y, después, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="0cfe4-118">Open the SQL Database Migration Wizard, on the **Select Process** page, select **Database under Analyze/Migrate**, and then click **Next**.</span></span>

   ![Asistente para migración de Base de datos SQL: seleccionar proceso](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/1.png)

3. <span data-ttu-id="0cfe4-120">En el cuadro de diálogo **Conectar con el servidor** , aplique la configuración siguiente:</span><span class="sxs-lookup"><span data-stu-id="0cfe4-120">In the **Connect to Server** dialog box, apply the following settings:</span></span>

   * <span data-ttu-id="0cfe4-121">Nombre del servidor: **su servidor SQL**</span><span class="sxs-lookup"><span data-stu-id="0cfe4-121">Server name: **Your SQL server**</span></span>
   * <span data-ttu-id="0cfe4-122">Autenticación: **Autenticación de SQL Server**</span><span class="sxs-lookup"><span data-stu-id="0cfe4-122">Authentication: **SQL Server Authentication**</span></span>
   * <span data-ttu-id="0cfe4-123">Inicio de sesión: **sus datos de inicio de sesión**</span><span class="sxs-lookup"><span data-stu-id="0cfe4-123">Login: **Your login**</span></span>
   * <span data-ttu-id="0cfe4-124">Contraseña: **su contraseña**</span><span class="sxs-lookup"><span data-stu-id="0cfe4-124">Password: **Your password**</span></span>
   * <span data-ttu-id="0cfe4-125">**Master DB (List all databases)** [BD maestra (Enumerar todas las bases de datos)]</span><span class="sxs-lookup"><span data-stu-id="0cfe4-125">Database: **Master DB (List all databases)**</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0cfe4-126">De forma predeterminada, el asistente guarda la información de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="0cfe4-126">By default the wizard saves your login information.</span></span> <span data-ttu-id="0cfe4-127">Si no quiere que lo haga, seleccione **Forget Login Information (No recordar la información de inicio de sesión)**.</span><span class="sxs-lookup"><span data-stu-id="0cfe4-127">If you don't want it to, select **Forget Login Information**.</span></span>
   >
   
     ![Asistente para migración de base de datos SQL: seleccionar origen, paso 1](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/2.png)
4. <span data-ttu-id="0cfe4-129">En el cuadro de diálogo **Seleccionar origen**, seleccione el nombre de la base de datos que ha restaurado en la sección **Pasos de preparación** como el origen y, después, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="0cfe4-129">In the **Select Source** dialog box, select the restored database name from the **Preparation steps** section as your source, and then click **Next**.</span></span>
   
    ![Asistente para migración de base de datos SQL: seleccionar origen, paso 2](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/3.png)
5. <span data-ttu-id="0cfe4-131">En el cuadro de diálogo **Elegir objetos**, seleccione la opción **Seleccionar objetos de base de datos específicos** y, después, seleccione la tabla (o tablas) que quiera migrar al servidor de destino.</span><span class="sxs-lookup"><span data-stu-id="0cfe4-131">In the **Choose Objects** dialog box, select the **Select specific database objects** option, and then select the table(or tables) that you want to migrate to the target server.</span></span>
   <span data-ttu-id="0cfe4-132">![Asistente para migración de base de datos SQL: elegir objetos](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)</span><span class="sxs-lookup"><span data-stu-id="0cfe4-132">![SQL Database Migration wizard - Choose Objects](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)</span></span>
6. <span data-ttu-id="0cfe4-133">En la página **Resumen del Asistente para scripts**, haga clic en **Sí** cuando se le pregunte si está listo para generar un script de SQL.</span><span class="sxs-lookup"><span data-stu-id="0cfe4-133">On the **Script Wizard Summary** page, click **Yes** when you’re prompted about whether you’re ready to generate a SQL script.</span></span> <span data-ttu-id="0cfe4-134">También tiene la opción de guardar el script TSQL para usarlo más adelante.</span><span class="sxs-lookup"><span data-stu-id="0cfe4-134">You also have the option to save the TSQL Script for later use.</span></span>
   <span data-ttu-id="0cfe4-135">![Asistente para migración de base de datos SQL: resumen del Asistente de scripts](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)</span><span class="sxs-lookup"><span data-stu-id="0cfe4-135">![SQL Database Migration wizard - Script Wizard Summary](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)</span></span>
7. <span data-ttu-id="0cfe4-136">En la página **Results Summary** (Resumen de resultados), haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="0cfe4-136">On the **Results Summary** page, click **Next**.</span></span>
   <span data-ttu-id="0cfe4-137">![Asistente para migración de base de datos SQL: resumen de resultados](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)</span><span class="sxs-lookup"><span data-stu-id="0cfe4-137">![SQL Database Migration wizard - Results Summary](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)</span></span>
8. <span data-ttu-id="0cfe4-138">En la página **Setup Target Server Connection** (Configurar conexión del servidor de destino), haga clic en **Conectar con el servidor** y, después, escriba los detalles de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="0cfe4-138">On the **Setup Target Server Connection** page, click **Connect to Server**, and then enter the details as follows:</span></span>
   
   * <span data-ttu-id="0cfe4-139">**Nombre del servidor**: instancia de servidor de destino</span><span class="sxs-lookup"><span data-stu-id="0cfe4-139">**Server Name**: Target server instance</span></span>
   * <span data-ttu-id="0cfe4-140">**Autenticación**: **Autenticación de SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="0cfe4-140">**Authentication**: **SQL Server authentication**.</span></span> <span data-ttu-id="0cfe4-141">Escriba sus credenciales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="0cfe4-141">Enter your login credentials.</span></span>
   * <span data-ttu-id="0cfe4-142">**Base de datos**: **Master DB (List all databases)** [BD maestra (Enumerar todas las bases de datos)].</span><span class="sxs-lookup"><span data-stu-id="0cfe4-142">**Database**: **Master DB (List all databases)**.</span></span> <span data-ttu-id="0cfe4-143">Esta opción enumera todas las bases de datos del servidor de destino.</span><span class="sxs-lookup"><span data-stu-id="0cfe4-143">This option lists all the databases on the target server.</span></span>
     
     ![Asistente para migración de base de datos SQL: configurar conexión del servidor de destino](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/7.png)
9. <span data-ttu-id="0cfe4-145">Haga clic en **Conectar**, seleccione la base de datos de destino a la que desea mover la tabla y, después, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="0cfe4-145">Click **Connect**, select the target database that you want to move the table to, and then click **Next**.</span></span> <span data-ttu-id="0cfe4-146">Esto debe finalizar con la ejecución del script generado anteriormente, y debería ver una copia de la tabla que se ha movido recientemente en la base de datos de destino.</span><span class="sxs-lookup"><span data-stu-id="0cfe4-146">This should finish running the previously generated script, and you should see the newly moved table copied to the target database.</span></span>

## <a name="verification-step"></a><span data-ttu-id="0cfe4-147">Paso de comprobación</span><span class="sxs-lookup"><span data-stu-id="0cfe4-147">Verification step</span></span>

- <span data-ttu-id="0cfe4-148">Consulte y pruebe la tabla copiada recientemente para asegurarse de que los datos estén intactos.</span><span class="sxs-lookup"><span data-stu-id="0cfe4-148">Query and test the newly copied table to make sure that the data is intact.</span></span> <span data-ttu-id="0cfe4-149">Tras la confirmación, puede deshacerse de la tabla a la que ha cambiado el nombre en la sección **Pasos de preparación**.</span><span class="sxs-lookup"><span data-stu-id="0cfe4-149">Upon confirmation, you can drop the renamed table form **Preparation steps** section.</span></span> <span data-ttu-id="0cfe4-150">(por ejemplo, &lt;nombre de la tabla&gt;_old).</span><span class="sxs-lookup"><span data-stu-id="0cfe4-150">(for example, &lt;table name&gt;_old).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0cfe4-151">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0cfe4-151">Next steps</span></span>
[<span data-ttu-id="0cfe4-152">Información general: copias de seguridad automatizadas de Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="0cfe4-152">SQL Database automatic backups</span></span>](sql-database-automated-backups.md)

