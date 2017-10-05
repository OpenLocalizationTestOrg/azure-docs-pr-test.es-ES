---
title: "Introducción a SQL Data Sync de Azure (versión preliminar) | Microsoft Docs"
description: "Este tutorial le ayuda a comenzar con Azure SQL Data Sync (versión preliminar)."
services: sql-database
documentationcenter: 
author: douglaslms
manager: craigg
editor: 
ms.assetid: a295a768-7ff2-4a86-a253-0090281c8efa
ms.service: sql-database
ms.custom: load & move data
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: douglasl
ms.openlocfilehash: 2d0f9d7f32ad79f49d58165d734b9df4af862835
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="getting-started-with-azure-sql-data-sync-preview"></a><span data-ttu-id="0fcf0-103">Introducción a SQL Data Sync de Azure (vista previa)</span><span class="sxs-lookup"><span data-stu-id="0fcf0-103">Getting Started with Azure SQL Data Sync (Preview)</span></span>
<span data-ttu-id="0fcf0-104">En este tutorial, obtendrá información sobre cómo configurar Azure SQL Data Sync mediante la creación de un grupo de sincronización híbrido que contiene instancias de Azure SQL Database y de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-104">In this tutorial, you learn how to set up Azure SQL Data Sync by creating a hybrid sync group that contains both Azure SQL Database and SQL Server instances.</span></span> <span data-ttu-id="0fcf0-105">El nuevo grupo de sincronización está configurado completamente y se sincroniza según el programa establecido.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-105">The new sync group is fully configured and synchronizes on the schedule you set.</span></span>

<span data-ttu-id="0fcf0-106">En este tutorial se asume que tiene al menos alguna experiencia previa con SQL Database y con SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-106">This tutorial assumes that you have at least some prior experience with SQL Database and with SQL Server.</span></span> 

<span data-ttu-id="0fcf0-107">Para obtener información general sobre SQL Data Sync, vea [Sincronización de datos](sql-database-sync-data.md).</span><span class="sxs-lookup"><span data-stu-id="0fcf0-107">For an overview of SQL Data Sync, see [Sync data](sql-database-sync-data.md).</span></span>

<span data-ttu-id="0fcf0-108">Para obtener ejemplos completos de PowerShell que muestren cómo configurar SQL Data Sync, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="0fcf0-108">For complete PowerShell examples that show how to configure SQL Data Sync, see the following articles:</span></span>
-   [<span data-ttu-id="0fcf0-109">Uso de PowerShell para sincronizar varias bases de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="0fcf0-109">Use PowerShell to sync between multiple Azure SQL databases</span></span>](scripts/sql-database-sync-data-between-sql-databases.md)
-   [<span data-ttu-id="0fcf0-110">Uso de PowerShell para sincronizar una base de datos SQL de Azure y una base de datos de SQL Server local</span><span class="sxs-lookup"><span data-stu-id="0fcf0-110">Use PowerShell to sync between an Azure SQL Database and a SQL Server on-premises database</span></span>](scripts/sql-database-sync-data-between-azure-onprem.md)

> [!NOTE]
> <span data-ttu-id="0fcf0-111">La documentación técnica completa para Azure SQL Data Sync, que anteriormente se encontraba en MSDN, está disponible como documento .pdf.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-111">The complete technical documentation set for Azure SQL Data Sync, formerly located on MSDN, is available as a .PDF document.</span></span> <span data-ttu-id="0fcf0-112">Descárguela [aquí](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true).</span><span class="sxs-lookup"><span data-stu-id="0fcf0-112">Download it [here](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true).</span></span>

## <a name="step-1---create-sync-group"></a><span data-ttu-id="0fcf0-113">Paso 1: Creación de un grupo de sincronización</span><span class="sxs-lookup"><span data-stu-id="0fcf0-113">Step 1 - Create sync group</span></span>

### <a name="locate-the-data-sync-settings"></a><span data-ttu-id="0fcf0-114">Búsqueda de la configuración de Data Sync</span><span class="sxs-lookup"><span data-stu-id="0fcf0-114">Locate the Data Sync settings</span></span>

1.  <span data-ttu-id="0fcf0-115">En el explorador, vaya a Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-115">In your browser, navigate to the Azure portal.</span></span>

2.  <span data-ttu-id="0fcf0-116">En el portal, busque las bases de datos SQL desde el panel o el icono de SQL Database de la barra de herramientas.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-116">In the portal, locate your SQL databases from your Dashboard or from the SQL Databases icon on the toolbar.</span></span>

    ![Lista de instancias de Azure SQL Database](media/sql-database-get-started-sql-data-sync/datasync-preview-sqldbs.png)

3.  <span data-ttu-id="0fcf0-118">En la hoja **SQL Database**, seleccione la instancia existente de SQL Database que desea utilizar como la base de datos central de Data Sync. Se abre la hoja de SQL Database.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-118">On the **SQL databases** blade, select the existing SQL database that you want to use as the hub database for Data Sync. The SQL database blade opens.</span></span>

4.  <span data-ttu-id="0fcf0-119">En la hoja de SQL Database para la base de datos seleccionada, seleccione **Sincronizar con otras bases de datos**.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-119">On the SQL database blade for the selected database, select **Sync to other databases**.</span></span> <span data-ttu-id="0fcf0-120">Se abre la hoja de Data Sync.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-120">The Data Sync blade opens.</span></span>

    ![Opción Sincronizar con otras bases de datos](media/sql-database-get-started-sql-data-sync/datasync-preview-newsyncgroup.png)

### <a name="create-a-new-sync-group"></a><span data-ttu-id="0fcf0-122">Creación de un grupo de sincronización</span><span class="sxs-lookup"><span data-stu-id="0fcf0-122">Create a new Sync Group</span></span>

1.  <span data-ttu-id="0fcf0-123">En la hoja de Data Sync, seleccione **Nuevo grupo de sincronización**.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-123">On the Data Sync blade, select **New Sync Group**.</span></span> <span data-ttu-id="0fcf0-124">La hoja **Nuevo grupo de sincronización** se abre con el paso 1, con **Crear grupo de sincronización** resaltado.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-124">The **New sync group** blade opens with Step 1, **Create sync group**, highlighted.</span></span> <span data-ttu-id="0fcf0-125">La hoja **Crear grupo de sincronización de datos** también se abre.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-125">The **Create Data Sync Group** blade also opens.</span></span>

2.  <span data-ttu-id="0fcf0-126">En la hoja **Crear grupo de sincronización de datos**, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="0fcf0-126">On the **Create Data Sync Group** blade, do the following things:</span></span>

    1.  <span data-ttu-id="0fcf0-127">En el campo **Nombre del grupo de sincronización**, escriba un nombre para el nuevo grupo de sincronización.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-127">In the **Sync Group Name** field, enter a name for the new sync group.</span></span>

    2.  <span data-ttu-id="0fcf0-128">En la sección **Base de datos de metadatos de sincronización**, elija si desea crear una base de datos (opción recomendada) o usar una existente.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-128">In the **Sync Metadata Database** section, choose whether to create a new database (recommended) or to use an existing database.</span></span>

        > [!NOTE]
        > <span data-ttu-id="0fcf0-129">Se recomienda crear una vacía para usarla como base de datos de metadatos de sincronización.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-129">Microsoft recommends that you create a new, empty database to use as the Sync Metadata Database.</span></span> <span data-ttu-id="0fcf0-130">Data Sync crea tablas en esta base de datos y ejecuta una carga de trabajo frecuente.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-130">Data Sync creates tables in this database and runs a frequent workload.</span></span> <span data-ttu-id="0fcf0-131">Esta base de datos se comparte automáticamente como la base de datos de metadatos de sincronización para todos los grupos de sincronización en la región seleccionada.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-131">This database is automatically shared as the Sync Metadata Database for all of your Sync groups in the selected region.</span></span> <span data-ttu-id="0fcf0-132">No se puede cambiar la base de datos de metadatos de sincronización, su nombre ni su nivel de servicio sin quitarla.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-132">You can't change the Sync Metadata Database, its name, or its service level without dropping it.</span></span>

        <span data-ttu-id="0fcf0-133">Si ha elegido **Nueva base de datos**, seleccione **Crear nueva base de datos**.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-133">If you chose **New database**, select **Create new database.**</span></span> <span data-ttu-id="0fcf0-134">Se abre la hoja de **SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-134">The **SQL Database** blade opens.</span></span> <span data-ttu-id="0fcf0-135">En la hoja **SQL Database**, asigne un nombre a la base de datos nueva y configúrela.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-135">On the **SQL Database** blade, name and configure the new database.</span></span> <span data-ttu-id="0fcf0-136">Después seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-136">Then select **OK**.</span></span>

        <span data-ttu-id="0fcf0-137">Si ha elegido **Usar base de datos existente**, seleccione la base de datos de la lista.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-137">If you chose **Use existing database**, select the database from the list.</span></span>

    3.  <span data-ttu-id="0fcf0-138">En la sección **Sincronización automática**, primero seleccione **Activado** o **Desactivado**.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-138">In the **Automatic Sync** section, first select **On** or **Off**.</span></span>

        <span data-ttu-id="0fcf0-139">Si ha elegido **Activado**, en la sección **Frecuencia de sincronización**, escriba un número y seleccione Segundos, Minutos, Horas o Días.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-139">If you chose **On**, in the **Sync Frequency** section, enter a number and select Seconds, Minutes, Hours, or Days.</span></span>

        ![Establecimiento de la frecuencia de sincronizaicón](media/sql-database-get-started-sql-data-sync/datasync-preview-syncfreq.png)

    4.  <span data-ttu-id="0fcf0-141">En la sección **Resolución de conflictos**, seleccione "Prevalece la base de datos central" o "Prevalece el cliente".</span><span class="sxs-lookup"><span data-stu-id="0fcf0-141">In the **Conflict Resolution** section, select "Hub wins" or "Member wins."</span></span>

        ![Especifique cómo se resuelven los conflictos](media/sql-database-get-started-sql-data-sync/datasync-preview-conflictres.png)

    5.  <span data-ttu-id="0fcf0-143">Seleccione **Aceptar** y espere a que el nuevo grupo de sincronización se cree e implemente.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-143">Select **OK** and wait for the new sync group to be created and deployed.</span></span>

## <a name="step-2---add-sync-members"></a><span data-ttu-id="0fcf0-144">Paso 2: Adición de miembros de sincronización</span><span class="sxs-lookup"><span data-stu-id="0fcf0-144">Step 2 - Add sync members</span></span>

<span data-ttu-id="0fcf0-145">Después de que el nuevo grupo de sincronización se crea e implementa, el paso 2, **Adición de miembros de sincronización**, se resalta en la hoja **Nuevo grupo de sincronización**.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-145">After the new sync group is created and deployed, Step 2, **Add sync members**, is highlighted in the **New sync group** blade.</span></span>

<span data-ttu-id="0fcf0-146">En la sección **Base de datos central**, escriba las credenciales existentes para el servidor de SQL Database en el que se encuentra la base de datos central.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-146">In the **Hub Database** section, enter the existing credentials for the SQL Database server on which the hub database is located.</span></span> <span data-ttu-id="0fcf0-147">No escriba *nuevas* credenciales en esta sección.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-147">Don't enter *new* credentials in this section.</span></span>

![La base de datos central se ha agregado al grupo de sincronización](media/sql-database-get-started-sql-data-sync/datasync-preview-hubadded.png)

## <a name="add-an-azure-sql-database"></a><span data-ttu-id="0fcf0-149">Adición de una instancia de Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="0fcf0-149">Add an Azure SQL Database</span></span>

<span data-ttu-id="0fcf0-150">En la sección **Base de datos de miembros**, tiene la opción de agregar una instancia de Azure SQL Database al grupo de sincronización si selecciona **Agregar una base de datos de Azure**.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-150">In the **Member Database** section, optionally add an Azure SQL Database to the sync group by selecting **Add an Azure Database**.</span></span> <span data-ttu-id="0fcf0-151">La hoja **Configurar base de datos de Azure** se abre.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-151">The **Configure Azure Database** blade opens.</span></span>

<span data-ttu-id="0fcf0-152">En la hoja **Configurar base de datos de Azure**, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="0fcf0-152">On the **Configure Azure Database** blade, do the following things:</span></span>

1.  <span data-ttu-id="0fcf0-153">En el campo **Nombre del miembro de sincronización**, proporcione un nombre para el nuevo miembro de sincronización.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-153">In the **Sync Member Name** field, provide a name for the new sync member.</span></span> <span data-ttu-id="0fcf0-154">Este nombre es distinto del nombre de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-154">This name is distinct from the name of the database itself.</span></span>

2.  <span data-ttu-id="0fcf0-155">En el campo **Suscripción**, seleccione la suscripción de Azure asociada para fines de facturación.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-155">In the **Subscription** field, select the associated Azure subscription for billing purposes.</span></span>

3.  <span data-ttu-id="0fcf0-156">En el campo **Azure SQL Server**, seleccione el servidor de SQL Database existente.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-156">In the **Azure SQL Server** field, select the existing SQL database server.</span></span>

4.  <span data-ttu-id="0fcf0-157">En el campo **Azure SQL Database**, seleccione la base de datos SQL existente.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-157">In the **Azure SQL Database** field, select the existing SQL database.</span></span>

5.  <span data-ttu-id="0fcf0-158">En el campo **Direcciones de sincronización**, seleccione la sincronización bidireccional, a la base de datos central o desde la base de datos central.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-158">In the **Sync Directions** field, select Bi-directional Sync, To the Hub, or From the Hub.</span></span>

    ![Adición de un nuevo miembro de sincronización de SQL Database](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadding.png)

6.  <span data-ttu-id="0fcf0-160">En los campos **Nombre de usuario** y **Contraseña**, escriba las credenciales existentes para el servidor de SQL Database en el que se encuentra la base de datos miembro.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-160">In the **Username** and **Password** fields, enter the existing credentials for the SQL Database server on which the member database is located.</span></span> <span data-ttu-id="0fcf0-161">No escriba *nuevas* credenciales en esta sección.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-161">Don't enter *new* credentials in this section.</span></span>

7.  <span data-ttu-id="0fcf0-162">Seleccione **Aceptar** y espere a que el nuevo miembro de sincronización se cree e implemente.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-162">Select **OK** and wait for the new sync member to be created and deployed.</span></span>

    ![Se ha agregado el nuevo miembro de sincronización de SQL Database](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadded.png)

## <a name="add-an-on-premises-sql-server-database"></a><span data-ttu-id="0fcf0-164">Adición de una base de datos local de SQL Server</span><span class="sxs-lookup"><span data-stu-id="0fcf0-164">Add an on-premises SQL Server database</span></span>

<span data-ttu-id="0fcf0-165">En la sección **Base de datos de miembros**, tiene la opción de agregar una instancia local de SQL Server al grupo de sincronización; para ello, seleccione **Agregar una base de datos local**.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-165">In the **Member Database** section, optionally add an on-premises SQL Server to the sync group by selecting **Add an On-Premises Database**.</span></span> <span data-ttu-id="0fcf0-166">La hoja **Configurar localmente** se abre.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-166">The **Configure On-Premises** blade opens.</span></span>

<span data-ttu-id="0fcf0-167">En la hoja **Configurar localmente**, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="0fcf0-167">On the **Configure On-Premises** blade, do the following things:</span></span>

1.  <span data-ttu-id="0fcf0-168">Seleccione **Elegir Sync Agent Gateway**.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-168">Select **Choose the Sync Agent Gateway**.</span></span> <span data-ttu-id="0fcf0-169">La hoja **Seleccionar agente de sincronización** se abre.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-169">The **Select Sync Agent** blade opens.</span></span>

    ![Selección de Sync Agent Gateway](media/sql-database-get-started-sql-data-sync/datasync-preview-choosegateway.png)

2.  <span data-ttu-id="0fcf0-171">En la hoja **Elegir Sync Agent Gateway**, elija si desea usar un agente existente o crear uno.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-171">On the **Choose the Sync Agent Gateway** blade, choose whether to use an existing agent or create a new agent.</span></span>

    <span data-ttu-id="0fcf0-172">Si ha elegido **Agentes existentes**, seleccione el agente existente en la lista.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-172">If you chose **Existing agents**, select the existing agent from the list.</span></span>

    <span data-ttu-id="0fcf0-173">Si ha elegido **Crear un agente nuevo**, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="0fcf0-173">If you chose **Create a new agent**, do the following things:</span></span>

    1.  <span data-ttu-id="0fcf0-174">Descargue el software del Agente de sincronización cliente del vínculo facilitado e instálelo en el equipo en que se encuentra SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-174">Download the client sync agent software from the link provided and install it on the computer where the SQL Server is located.</span></span>
 
        > [!IMPORTANT]
        > <span data-ttu-id="0fcf0-175">Tendrá que abrir el puerto TCP 1433 saliente en el firewall para permitir que el agente cliente se comunique con el servidor.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-175">You have to open outbound TCP port 1433 in the firewall to let the client agent communicate with the server.</span></span>


    2.  <span data-ttu-id="0fcf0-176">Escriba un nombre para el agente.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-176">Enter a name for the agent.</span></span>

    3.  <span data-ttu-id="0fcf0-177">Seleccione **Crear y generar clave**.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-177">Select **Create and Generate Key**.</span></span>

    4.  <span data-ttu-id="0fcf0-178">Copie la clave del agente en el Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-178">Copy the agent key to the clipboard.</span></span>
        
        ![Creación de un agente de sincronización](media/sql-database-get-started-sql-data-sync/datasync-preview-selectsyncagent.png)

    5.  <span data-ttu-id="0fcf0-180">Seleccione **Aceptar** para cerrar la hoja **Seleccionar agente de sincronización**.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-180">Select **OK** to close the **Select Sync Agent** blade.</span></span>

    6.  <span data-ttu-id="0fcf0-181">En el equipo de SQL Server, localice y ejecute la aplicación del Agente de sincronización cliente.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-181">On the SQL Server computer, locate and run the Client Sync Agent app.</span></span>

        ![La aplicación del agente cliente de Data Sync](media/sql-database-get-started-sql-data-sync/datasync-preview-clientagent.png)

    7.  <span data-ttu-id="0fcf0-183">En la aplicación del agente de sincronización, seleccione **Enviar clave del agente**.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-183">In the sync agent app, select **Submit Agent Key**.</span></span> <span data-ttu-id="0fcf0-184">Se abre el cuadro de diálogo **Configuración de base de datos de metadatos de sincronización**.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-184">The **Sync Metadata Database Configuration** dialog box opens.</span></span>

    8.  <span data-ttu-id="0fcf0-185">En el cuadro de diálogo **Configuración de base de datos de metadatos de sincronización**, pegue la clave del agente copiada de Azure Portal,</span><span class="sxs-lookup"><span data-stu-id="0fcf0-185">In the **Sync Metadata Database Configuration** dialog box, paste in the agent key copied from the Azure portal.</span></span> <span data-ttu-id="0fcf0-186">Proporcione también las credenciales existentes para el servidor de Azure SQL Database en el que se encuentra la base de datos de metadatos.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-186">Also provide the existing credentials for the Azure SQL Database server on which the metadata database is located.</span></span> <span data-ttu-id="0fcf0-187">(Si ha creado una base de datos de metadatos, esta base de datos está en el mismo servidor que la base de datos central). Seleccione **Aceptar** y espere a que la configuración finalice.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-187">(If you created a new metadata database, this database is on the same server as the hub database.) Select **OK** and wait for the configuration to finish.</span></span>

        ![Definición de las credenciales del servidor y de la clave del agente](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-enterkey.png)

        >   [!NOTE] 
        >   <span data-ttu-id="0fcf0-189">Si recibe un error de firewall en este punto, tendrá que crear una regla de firewall en Azure para permitir el tráfico entrante desde el equipo de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-189">If you get a firewall error at this point, you have to create a firewall rule on Azure to allow incoming traffic from the SQL Server computer.</span></span> <span data-ttu-id="0fcf0-190">Puede crear manualmente la regla en el portal, pero quizá le resulte más fácil crearla en SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="0fcf0-190">You can create the rule manually in the portal, but you may find it easier to create it in SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="0fcf0-191">En SSMS, intente conectarse a la base de datos central en Azure.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-191">In SSMS, try to connect to the hub database on Azure.</span></span> <span data-ttu-id="0fcf0-192">Escriba su nombre como \<hub_database_name\>.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-192">Enter its name as \<hub_database_name\>.database.windows.net.</span></span> <span data-ttu-id="0fcf0-193">Siga los pasos del cuadro de diálogo para configurar la regla de firewall de Azure.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-193">Follow the steps in the dialog box to configure the Azure firewall rule.</span></span> <span data-ttu-id="0fcf0-194">A continuación, vuelva a la aplicación de Agente de sincronización cliente.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-194">Then return to the Client Sync Agent app.</span></span>

    9.  <span data-ttu-id="0fcf0-195">En la aplicación del Agente de sincronización cliente, haga clic en **Registrar** para registrar una instancia de SQL Server Database en el agente.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-195">In the Client Sync Agent app, click **Register** to register a SQL Server database with the agent.</span></span> <span data-ttu-id="0fcf0-196">Se abre el cuadro de diálogo **Configuración de SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-196">The **SQL Server Configuration** dialog box opens.</span></span>

        ![Adición y configuración de una instancia de SQL Server Database](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-adddb.png)

    10. <span data-ttu-id="0fcf0-198">En el cuadro de diálogo **Configuración de SQL Server**, elija si desea conectarse mediante autenticación de SQL Server o autenticación de Windows.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-198">In the **SQL Server Configuration** dialog box, choose whether to connect by using SQL Server authentication or Windows authentication.</span></span> <span data-ttu-id="0fcf0-199">Si elige la autenticación de SQL Server, escriba las credenciales existentes.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-199">If you chose SQL Server authentication, enter the existing credentials.</span></span> <span data-ttu-id="0fcf0-200">Proporcione el nombre de SQL Server y el nombre de la base de datos que desea sincronizar. Seleccione **Probar conexión** para probar la configuración.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-200">Provide the SQL Server name and the name of the database that you want to sync. Select **Test connection** to test your settings.</span></span> <span data-ttu-id="0fcf0-201">Después, seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-201">Then select **Save**.</span></span> <span data-ttu-id="0fcf0-202">La base de datos registrada aparece en la lista.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-202">The registered database appears in the list.</span></span>

        ![La base de datos de SQL Server ya está registrada](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-dbadded.png)

    11. <span data-ttu-id="0fcf0-204">Ahora puede cerrar la aplicación del Agente de sincronización cliente.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-204">You can now close the Client Sync Agent app.</span></span>

    12. <span data-ttu-id="0fcf0-205">En el portal, en la hoja **Configurar localmente**, seleccione **Seleccionar una base de datos**.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-205">In the portal, on the **Configure On-Premises** blade, select **Select the Database.**</span></span> <span data-ttu-id="0fcf0-206">Se abre la hoja de **Seleccionar una base de datos**.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-206">The **Select Database** blade opens.</span></span>

    13. <span data-ttu-id="0fcf0-207">En la hoja **Seleccionar una base de datos**, en el campo **Nombre del miembro de sincronización**, proporcione un nombre para el nuevo miembro de sincronización.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-207">On the **Select Database** blade, in the **Sync Member Name** field, provide a name for the new sync member.</span></span> <span data-ttu-id="0fcf0-208">Este nombre es distinto del nombre de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-208">This name is distinct from the name of the database itself.</span></span> <span data-ttu-id="0fcf0-209">Seleccione la base de datos de la lista.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-209">Select the database from the list.</span></span> <span data-ttu-id="0fcf0-210">En el campo **Direcciones de sincronización**, seleccione la sincronización bidireccional, a la base de datos central o desde la base de datos central.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-210">In the **Sync Directions** field, select Bi-directional Sync, To the Hub, or From the Hub.</span></span>

        ![Seleccione la base de datos local](media/sql-database-get-started-sql-data-sync/datasync-preview-selectdb.png)

    14. <span data-ttu-id="0fcf0-212">Seleccione **Aceptar** para cerrar la hoja **Seleccionar una base de datos**.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-212">Select **OK** to close the **Select Database** blade.</span></span> <span data-ttu-id="0fcf0-213">Después, seleccione **Aceptar** para cerrar la hoja **Configurar localmente** y espere a que el nuevo miembro de sincronización se cree e implemente.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-213">Then select **OK** to close the **Configure On-Premises** blade and wait for the new sync member to be created and deployed.</span></span> <span data-ttu-id="0fcf0-214">Por último, haga clic en **Aceptar** para cerrar la hoja **Seleccionar miembros de sincronización**.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-214">Finally, click **OK** to close the **Select sync members** blade.</span></span>

        ![Base de datos local agregada al grupo de sincronización](media/sql-database-get-started-sql-data-sync/datasync-preview-onpremadded.png)

3.  <span data-ttu-id="0fcf0-216">Para conectarse a SQL Data Sync y al agente local, agregue el nombre de usuario al rol `DataSync_Executor`.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-216">To connect to SQL Data Sync and the local agent, add your user name to the role `DataSync_Executor`.</span></span> <span data-ttu-id="0fcf0-217">Data Sync crea este rol en la instancia de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-217">Data Sync creates this role on the SQL Server instance.</span></span>

## <a name="step-3---configure-sync-group"></a><span data-ttu-id="0fcf0-218">Paso 3: Configuración del grupo de sincronización</span><span class="sxs-lookup"><span data-stu-id="0fcf0-218">Step 3 - Configure sync group</span></span>

<span data-ttu-id="0fcf0-219">Después de que los nuevos miembros del grupo de sincronización se crean e implementan, el paso 3, **Configuración del grupo de sincronización**, se resalta en la hoja **Nuevo grupo de sincronización**.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-219">After the new sync group members are created and deployed, Step 3, **Configure sync group**, is highlighted in the **New sync group** blade.</span></span>

1.  <span data-ttu-id="0fcf0-220">En la hoja **Tablas**, seleccione una base de datos en la lista de miembros del grupo de sincronización y, después, seleccione **Actualizar esquema**.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-220">On the **Tables** blade, select a database from the list of sync group members, and then select **Refresh schema**.</span></span>

2.  <span data-ttu-id="0fcf0-221">En la lista de tablas disponibles, seleccione las tablas que desea sincronizar.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-221">From the list of available tables, select the tables that you want to sync.</span></span>

    ![Selección de tablas para sincronizar](media/sql-database-get-started-sql-data-sync/datasync-preview-tables.png)

3.  <span data-ttu-id="0fcf0-223">De forma predeterminada, se seleccionan todas las columnas de la tabla.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-223">By default, all columns in the table are selected.</span></span> <span data-ttu-id="0fcf0-224">Si no desea sincronizar todas las columnas, deshabilite la casilla de las columnas que no desea sincronizar. Asegúrese de dejar seleccionada la columna de clave principal.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-224">If you don't want to sync all the columns, disable the checkbox for the columns that you don't want to sync. Be sure to leave the primary key column selected.</span></span>

    ![Selección de campos para sincronizar](media/sql-database-get-started-sql-data-sync/datasync-preview-tables2.png)

4.  <span data-ttu-id="0fcf0-226">Por último, seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-226">Finally, select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0fcf0-227">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0fcf0-227">Next steps</span></span>
<span data-ttu-id="0fcf0-228">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="0fcf0-228">Congratulations.</span></span> <span data-ttu-id="0fcf0-229">Ha creado un grupo de sincronización que incluye una instancia de SQL Database y una base de datos de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0fcf0-229">You have created a sync group that includes both a SQL Database instance and a SQL Server database.</span></span>

<span data-ttu-id="0fcf0-230">Para obtener más información sobre SQL Database y SQL Data Sync, vea:</span><span class="sxs-lookup"><span data-stu-id="0fcf0-230">For more info about SQL Database and SQL Data Sync, see:</span></span>

-   [<span data-ttu-id="0fcf0-231">Descarga de la documentación técnica completa de SQL Data Sync</span><span class="sxs-lookup"><span data-stu-id="0fcf0-231">Download the complete SQL Data Sync technical documentation</span></span>](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)
-   [<span data-ttu-id="0fcf0-232">Descarga de la documentación de la API de REST de SQL Data Sync</span><span class="sxs-lookup"><span data-stu-id="0fcf0-232">Download the SQL Data Sync REST API documentation</span></span>](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)
-   [<span data-ttu-id="0fcf0-233">Información general de SQL Database</span><span class="sxs-lookup"><span data-stu-id="0fcf0-233">SQL Database Overview</span></span>](sql-database-technical-overview.md)
-   [<span data-ttu-id="0fcf0-234">Administración del ciclo de vida de las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="0fcf0-234">Database Lifecycle Management</span></span>](https://msdn.microsoft.com/library/jj907294.aspx)
