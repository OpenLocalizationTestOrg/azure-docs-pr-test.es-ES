---
title: "aaaGetting a trabajar con Azure SQL Data Sync (versión preliminar) | Documentos de Microsoft"
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
ms.openlocfilehash: 666d09237e42acc23ae3c8c81e60734a413f5949
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-sql-data-sync-preview"></a><span data-ttu-id="9bee6-103">Introducción a SQL Data Sync de Azure (vista previa)</span><span class="sxs-lookup"><span data-stu-id="9bee6-103">Getting Started with Azure SQL Data Sync (Preview)</span></span>
<span data-ttu-id="9bee6-104">En este tutorial, aprenderá cómo tooset la sincronización de datos de SQL Azure mediante la creación de un grupo de sincronización híbrida contiene instancias de base de datos de SQL Azure y SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9bee6-104">In this tutorial, you learn how tooset up Azure SQL Data Sync by creating a hybrid sync group that contains both Azure SQL Database and SQL Server instances.</span></span> <span data-ttu-id="9bee6-105">nuevo grupo de sincronización Hola esté completamente configurado y se sincroniza en programación Hola establecida.</span><span class="sxs-lookup"><span data-stu-id="9bee6-105">hello new sync group is fully configured and synchronizes on hello schedule you set.</span></span>

<span data-ttu-id="9bee6-106">En este tutorial se asume que tiene al menos alguna experiencia previa con SQL Database y con SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9bee6-106">This tutorial assumes that you have at least some prior experience with SQL Database and with SQL Server.</span></span> 

<span data-ttu-id="9bee6-107">Para obtener información general sobre SQL Data Sync, vea [Sincronización de datos](sql-database-sync-data.md).</span><span class="sxs-lookup"><span data-stu-id="9bee6-107">For an overview of SQL Data Sync, see [Sync data](sql-database-sync-data.md).</span></span>

<span data-ttu-id="9bee6-108">Para obtener ejemplos PowerShell completos que muestran cómo tooconfigure SQL Data Sync, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="9bee6-108">For complete PowerShell examples that show how tooconfigure SQL Data Sync, see hello following articles:</span></span>
-   [<span data-ttu-id="9bee6-109">Usar PowerShell toosync entre varias bases de datos de SQL Azure</span><span class="sxs-lookup"><span data-stu-id="9bee6-109">Use PowerShell toosync between multiple Azure SQL databases</span></span>](scripts/sql-database-sync-data-between-sql-databases.md)
-   [<span data-ttu-id="9bee6-110">Usar PowerShell toosync entre una base de datos de SQL Azure y una base de datos de SQL Server local</span><span class="sxs-lookup"><span data-stu-id="9bee6-110">Use PowerShell toosync between an Azure SQL Database and a SQL Server on-premises database</span></span>](scripts/sql-database-sync-data-between-azure-onprem.md)

> [!NOTE]
> <span data-ttu-id="9bee6-111">documentación técnica completa Hola establecido para la sincronización de datos de SQL Azure, anteriormente ubicada en MSDN, está disponible como un. Documento PDF.</span><span class="sxs-lookup"><span data-stu-id="9bee6-111">hello complete technical documentation set for Azure SQL Data Sync, formerly located on MSDN, is available as a .PDF document.</span></span> <span data-ttu-id="9bee6-112">Descárguela [aquí](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true).</span><span class="sxs-lookup"><span data-stu-id="9bee6-112">Download it [here](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true).</span></span>

## <a name="step-1---create-sync-group"></a><span data-ttu-id="9bee6-113">Paso 1: Creación de un grupo de sincronización</span><span class="sxs-lookup"><span data-stu-id="9bee6-113">Step 1 - Create sync group</span></span>

### <a name="locate-hello-data-sync-settings"></a><span data-ttu-id="9bee6-114">Busque la configuración de sincronización de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="9bee6-114">Locate hello Data Sync settings</span></span>

1.  <span data-ttu-id="9bee6-115">En el explorador, navegue toohello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9bee6-115">In your browser, navigate toohello Azure portal.</span></span>

2.  <span data-ttu-id="9bee6-116">En el portal de hello, busque las bases de datos SQL desde el panel o desde el icono de bases de datos SQL de hello en la barra de herramientas de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bee6-116">In hello portal, locate your SQL databases from your Dashboard or from hello SQL Databases icon on hello toolbar.</span></span>

    ![Lista de instancias de Azure SQL Database](media/sql-database-get-started-sql-data-sync/datasync-preview-sqldbs.png)

3.  <span data-ttu-id="9bee6-118">En hello **bases de datos SQL** hoja, seleccione Hola SQL base de datos existente que desee toouse abre la base de datos de hello central para datos de sincronización. hoja de base de datos SQL de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bee6-118">On hello **SQL databases** blade, select hello existing SQL database that you want toouse as hello hub database for Data Sync. hello SQL database blade opens.</span></span>

4.  <span data-ttu-id="9bee6-119">En la hoja de base de datos SQL de hello para la base de datos seleccionada de hello, seleccione **sincronizar bases de datos de tooother**.</span><span class="sxs-lookup"><span data-stu-id="9bee6-119">On hello SQL database blade for hello selected database, select **Sync tooother databases**.</span></span> <span data-ttu-id="9bee6-120">se abre la hoja de Data Sync de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bee6-120">hello Data Sync blade opens.</span></span>

    ![Opción de sincronización de bases de datos tooother](media/sql-database-get-started-sql-data-sync/datasync-preview-newsyncgroup.png)

### <a name="create-a-new-sync-group"></a><span data-ttu-id="9bee6-122">Creación de un grupo de sincronización</span><span class="sxs-lookup"><span data-stu-id="9bee6-122">Create a new Sync Group</span></span>

1.  <span data-ttu-id="9bee6-123">En la hoja de la sincronización de datos de hello, seleccione **nuevo grupo de sincronización**.</span><span class="sxs-lookup"><span data-stu-id="9bee6-123">On hello Data Sync blade, select **New Sync Group**.</span></span> <span data-ttu-id="9bee6-124">Hola **nuevo grupo de sincronización** hoja se abre con el paso 1, **crear grupo de sincronización**, resaltada.</span><span class="sxs-lookup"><span data-stu-id="9bee6-124">hello **New sync group** blade opens with Step 1, **Create sync group**, highlighted.</span></span> <span data-ttu-id="9bee6-125">Hola **crear grupo de sincronización de datos** también se abre la hoja.</span><span class="sxs-lookup"><span data-stu-id="9bee6-125">hello **Create Data Sync Group** blade also opens.</span></span>

2.  <span data-ttu-id="9bee6-126">En hello **crear grupo de sincronización de datos** hoja, Hola siguientes cosas:</span><span class="sxs-lookup"><span data-stu-id="9bee6-126">On hello **Create Data Sync Group** blade, do hello following things:</span></span>

    1.  <span data-ttu-id="9bee6-127">Hola **nombre del grupo de sincronización** , a continuación, escriba un nombre para el nuevo grupo de sincronización Hola.</span><span class="sxs-lookup"><span data-stu-id="9bee6-127">In hello **Sync Group Name** field, enter a name for hello new sync group.</span></span>

    2.  <span data-ttu-id="9bee6-128">Hola **base de datos de metadatos de sincronización** sección, elija si toocreate una nueva base de datos (recomendado) o toouse otra base de datos.</span><span class="sxs-lookup"><span data-stu-id="9bee6-128">In hello **Sync Metadata Database** section, choose whether toocreate a new database (recommended) or toouse an existing database.</span></span>

        > [!NOTE]
        > <span data-ttu-id="9bee6-129">Microsoft recomienda que cree una base de datos nueva y vacía toouse como Hola base de datos de metadatos de sincronización.</span><span class="sxs-lookup"><span data-stu-id="9bee6-129">Microsoft recommends that you create a new, empty database toouse as hello Sync Metadata Database.</span></span> <span data-ttu-id="9bee6-130">Data Sync crea tablas en esta base de datos y ejecuta una carga de trabajo frecuente.</span><span class="sxs-lookup"><span data-stu-id="9bee6-130">Data Sync creates tables in this database and runs a frequent workload.</span></span> <span data-ttu-id="9bee6-131">Esta base de datos se comparte automáticamente como base de datos de metadatos de sincronización para todos los grupos de sincronización en la región seleccionada de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="9bee6-131">This database is automatically shared as hello Sync Metadata Database for all of your Sync groups in hello selected region.</span></span> <span data-ttu-id="9bee6-132">No se puede cambiar base de datos de metadatos de sincronización de hello, su nombre o su nivel de servicio sin colocarlo.</span><span class="sxs-lookup"><span data-stu-id="9bee6-132">You can't change hello Sync Metadata Database, its name, or its service level without dropping it.</span></span>

        <span data-ttu-id="9bee6-133">Si ha elegido **Nueva base de datos**, seleccione **Crear nueva base de datos**.</span><span class="sxs-lookup"><span data-stu-id="9bee6-133">If you chose **New database**, select **Create new database.**</span></span> <span data-ttu-id="9bee6-134">Hola **base de datos SQL** abre la hoja.</span><span class="sxs-lookup"><span data-stu-id="9bee6-134">hello **SQL Database** blade opens.</span></span> <span data-ttu-id="9bee6-135">En hello **base de datos SQL** hoja, asigne un nombre y configurar Hola nueva base de datos.</span><span class="sxs-lookup"><span data-stu-id="9bee6-135">On hello **SQL Database** blade, name and configure hello new database.</span></span> <span data-ttu-id="9bee6-136">Después seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="9bee6-136">Then select **OK**.</span></span>

        <span data-ttu-id="9bee6-137">Si ha elegido **usar base de datos existente**, seleccione base de datos de hello en lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bee6-137">If you chose **Use existing database**, select hello database from hello list.</span></span>

    3.  <span data-ttu-id="9bee6-138">Hola **sincronización automática** , primero seleccione **en** o **desactivar**.</span><span class="sxs-lookup"><span data-stu-id="9bee6-138">In hello **Automatic Sync** section, first select **On** or **Off**.</span></span>

        <span data-ttu-id="9bee6-139">Si ha elegido **en**, Hola **frecuencia de sincronización** sección, escriba un número y seleccione segundos, minutos, horas o días.</span><span class="sxs-lookup"><span data-stu-id="9bee6-139">If you chose **On**, in hello **Sync Frequency** section, enter a number and select Seconds, Minutes, Hours, or Days.</span></span>

        ![Establecimiento de la frecuencia de sincronizaicón](media/sql-database-get-started-sql-data-sync/datasync-preview-syncfreq.png)

    4.  <span data-ttu-id="9bee6-141">Hola **la resolución de conflictos** sección, seleccione "Gana la central" o "Miembro wins."</span><span class="sxs-lookup"><span data-stu-id="9bee6-141">In hello **Conflict Resolution** section, select "Hub wins" or "Member wins."</span></span>

        ![Especifique cómo se resuelven los conflictos](media/sql-database-get-started-sql-data-sync/datasync-preview-conflictres.png)

    5.  <span data-ttu-id="9bee6-143">Seleccione **Aceptar** y espere Hola nueva sincronización grupo toobe creado e implementado.</span><span class="sxs-lookup"><span data-stu-id="9bee6-143">Select **OK** and wait for hello new sync group toobe created and deployed.</span></span>

## <a name="step-2---add-sync-members"></a><span data-ttu-id="9bee6-144">Paso 2: Adición de miembros de sincronización</span><span class="sxs-lookup"><span data-stu-id="9bee6-144">Step 2 - Add sync members</span></span>

<span data-ttu-id="9bee6-145">Después de que se crea e implementa, paso 2, grupo de sincronización hello **agregar miembros de sincronización**, se resalta en hello **nuevo grupo de sincronización** hoja.</span><span class="sxs-lookup"><span data-stu-id="9bee6-145">After hello new sync group is created and deployed, Step 2, **Add sync members**, is highlighted in hello **New sync group** blade.</span></span>

<span data-ttu-id="9bee6-146">Hola **base de datos central** sección, escriba las credenciales existentes de hello para el servidor de base de datos SQL de hello en qué Hola se encuentra la base de datos central.</span><span class="sxs-lookup"><span data-stu-id="9bee6-146">In hello **Hub Database** section, enter hello existing credentials for hello SQL Database server on which hello hub database is located.</span></span> <span data-ttu-id="9bee6-147">No escriba *nuevas* credenciales en esta sección.</span><span class="sxs-lookup"><span data-stu-id="9bee6-147">Don't enter *new* credentials in this section.</span></span>

![Base de datos central se ha agregado el grupo de toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-hubadded.png)

## <a name="add-an-azure-sql-database"></a><span data-ttu-id="9bee6-149">Adición de una instancia de Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="9bee6-149">Add an Azure SQL Database</span></span>

<span data-ttu-id="9bee6-150">Hola **base de datos miembro** sección, opcionalmente, agregar un grupo de sincronización de base de datos de SQL Azure toohello seleccionando **agregar una base de datos de Azure**.</span><span class="sxs-lookup"><span data-stu-id="9bee6-150">In hello **Member Database** section, optionally add an Azure SQL Database toohello sync group by selecting **Add an Azure Database**.</span></span> <span data-ttu-id="9bee6-151">Hola **Configurar base de datos de Azure** abre la hoja.</span><span class="sxs-lookup"><span data-stu-id="9bee6-151">hello **Configure Azure Database** blade opens.</span></span>

<span data-ttu-id="9bee6-152">En hello **Configurar base de datos de Azure** hoja, Hola siguientes cosas:</span><span class="sxs-lookup"><span data-stu-id="9bee6-152">On hello **Configure Azure Database** blade, do hello following things:</span></span>

1.  <span data-ttu-id="9bee6-153">Hola **nombre del miembro de sincronización** campo, proporcione un nombre para el nuevo miembro de sincronización Hola.</span><span class="sxs-lookup"><span data-stu-id="9bee6-153">In hello **Sync Member Name** field, provide a name for hello new sync member.</span></span> <span data-ttu-id="9bee6-154">Este nombre es distinto del nombre de Hola de hello propia base de datos.</span><span class="sxs-lookup"><span data-stu-id="9bee6-154">This name is distinct from hello name of hello database itself.</span></span>

2.  <span data-ttu-id="9bee6-155">Hola **suscripción** Hola de campo, seleccione asociados suscripción de Azure para fines de facturación.</span><span class="sxs-lookup"><span data-stu-id="9bee6-155">In hello **Subscription** field, select hello associated Azure subscription for billing purposes.</span></span>

3.  <span data-ttu-id="9bee6-156">Hola **Azure SQL Server** servidor de base de datos SQL existente, seleccione Hola.</span><span class="sxs-lookup"><span data-stu-id="9bee6-156">In hello **Azure SQL Server** field, select hello existing SQL database server.</span></span>

4.  <span data-ttu-id="9bee6-157">Hola **base de datos de SQL Azure** base de datos SQL existente Hola de campo, seleccione.</span><span class="sxs-lookup"><span data-stu-id="9bee6-157">In hello **Azure SQL Database** field, select hello existing SQL database.</span></span>

5.  <span data-ttu-id="9bee6-158">Hola **direcciones de sincronización** , a continuación, seleccionar la sincronización bidireccional, toohello concentrador, o de hello concentrador.</span><span class="sxs-lookup"><span data-stu-id="9bee6-158">In hello **Sync Directions** field, select Bi-directional Sync, toohello Hub, or From hello Hub.</span></span>

    ![Adición de un nuevo miembro de sincronización de SQL Database](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadding.png)

6.  <span data-ttu-id="9bee6-160">Hola **nombre de usuario** y **contraseña** campos, escriba las credenciales existentes de hello para el servidor de base de datos SQL de hello en qué Hola base de datos miembro se encuentra.</span><span class="sxs-lookup"><span data-stu-id="9bee6-160">In hello **Username** and **Password** fields, enter hello existing credentials for hello SQL Database server on which hello member database is located.</span></span> <span data-ttu-id="9bee6-161">No escriba *nuevas* credenciales en esta sección.</span><span class="sxs-lookup"><span data-stu-id="9bee6-161">Don't enter *new* credentials in this section.</span></span>

7.  <span data-ttu-id="9bee6-162">Seleccione **Aceptar** y espere Hola nueva sincronización miembro toobe creado e implementado.</span><span class="sxs-lookup"><span data-stu-id="9bee6-162">Select **OK** and wait for hello new sync member toobe created and deployed.</span></span>

    ![Se ha agregado el nuevo miembro de sincronización de SQL Database](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadded.png)

## <a name="add-an-on-premises-sql-server-database"></a><span data-ttu-id="9bee6-164">Adición de una base de datos local de SQL Server</span><span class="sxs-lookup"><span data-stu-id="9bee6-164">Add an on-premises SQL Server database</span></span>

<span data-ttu-id="9bee6-165">Hola **base de datos miembro** sección, opcionalmente, agregar un grupo de sincronización de toohello de SQL Server local seleccionando **agregar una base de datos local**.</span><span class="sxs-lookup"><span data-stu-id="9bee6-165">In hello **Member Database** section, optionally add an on-premises SQL Server toohello sync group by selecting **Add an On-Premises Database**.</span></span> <span data-ttu-id="9bee6-166">Hola **configurar local** abre la hoja.</span><span class="sxs-lookup"><span data-stu-id="9bee6-166">hello **Configure On-Premises** blade opens.</span></span>

<span data-ttu-id="9bee6-167">En hello **configurar local** hoja, Hola siguientes cosas:</span><span class="sxs-lookup"><span data-stu-id="9bee6-167">On hello **Configure On-Premises** blade, do hello following things:</span></span>

1.  <span data-ttu-id="9bee6-168">Seleccione **elegir Hola puerta de enlace de agente de sincronización**.</span><span class="sxs-lookup"><span data-stu-id="9bee6-168">Select **Choose hello Sync Agent Gateway**.</span></span> <span data-ttu-id="9bee6-169">Hola **seleccione Agente de sincronización** abre la hoja.</span><span class="sxs-lookup"><span data-stu-id="9bee6-169">hello **Select Sync Agent** blade opens.</span></span>

    ![Elegir puerta de enlace del agente de sincronización de Hola](media/sql-database-get-started-sql-data-sync/datasync-preview-choosegateway.png)

2.  <span data-ttu-id="9bee6-171">En hello **elegir Hola puerta de enlace de agente de sincronización** hoja, elija si toouse un agente existente o crear un nuevo agente.</span><span class="sxs-lookup"><span data-stu-id="9bee6-171">On hello **Choose hello Sync Agent Gateway** blade, choose whether toouse an existing agent or create a new agent.</span></span>

    <span data-ttu-id="9bee6-172">Si ha elegido **existente agentes**, seleccione Hola agente existente de la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bee6-172">If you chose **Existing agents**, select hello existing agent from hello list.</span></span>

    <span data-ttu-id="9bee6-173">Si ha elegido **crear un nuevo agente**, Hola siguientes cosas:</span><span class="sxs-lookup"><span data-stu-id="9bee6-173">If you chose **Create a new agent**, do hello following things:</span></span>

    1.  <span data-ttu-id="9bee6-174">Descargar software de agente de sincronización de cliente de Hola de vínculo de hello proporcionado e instalarlo en el equipo Hola donde se encuentra Hola SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9bee6-174">Download hello client sync agent software from hello link provided and install it on hello computer where hello SQL Server is located.</span></span>
 
        > [!IMPORTANT]
        > <span data-ttu-id="9bee6-175">Tener tooopen salida el puerto TCP 1433 en el agente de cliente de hello firewall toolet Hola comunicarse con el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bee6-175">You have tooopen outbound TCP port 1433 in hello firewall toolet hello client agent communicate with hello server.</span></span>


    2.  <span data-ttu-id="9bee6-176">Escriba un nombre para el agente de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bee6-176">Enter a name for hello agent.</span></span>

    3.  <span data-ttu-id="9bee6-177">Seleccione **Crear y generar clave**.</span><span class="sxs-lookup"><span data-stu-id="9bee6-177">Select **Create and Generate Key**.</span></span>

    4.  <span data-ttu-id="9bee6-178">Portapapeles de toohello clave de agente de copia Hola.</span><span class="sxs-lookup"><span data-stu-id="9bee6-178">Copy hello agent key toohello clipboard.</span></span>
        
        ![Creación de un agente de sincronización](media/sql-database-get-started-sql-data-sync/datasync-preview-selectsyncagent.png)

    5.  <span data-ttu-id="9bee6-180">Seleccione **Aceptar** tooclose hello **seleccione Agente de sincronización** hoja.</span><span class="sxs-lookup"><span data-stu-id="9bee6-180">Select **OK** tooclose hello **Select Sync Agent** blade.</span></span>

    6.  <span data-ttu-id="9bee6-181">En el equipo de SQL Server de hello, busque y ejecute la aplicación del agente de sincronización cliente hello.</span><span class="sxs-lookup"><span data-stu-id="9bee6-181">On hello SQL Server computer, locate and run hello Client Sync Agent app.</span></span>

        ![aplicación cliente de agente de sincronización de datos de Hola](media/sql-database-get-started-sql-data-sync/datasync-preview-clientagent.png)

    7.  <span data-ttu-id="9bee6-183">En la aplicación del agente de sincronización de hello, seleccione **Enviar clave del agente**.</span><span class="sxs-lookup"><span data-stu-id="9bee6-183">In hello sync agent app, select **Submit Agent Key**.</span></span> <span data-ttu-id="9bee6-184">Hola **configuración de base de datos de metadatos de sincronización** abre el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9bee6-184">hello **Sync Metadata Database Configuration** dialog box opens.</span></span>

    8.  <span data-ttu-id="9bee6-185">Hola **configuración de base de datos de metadatos de sincronización** cuadro de diálogo, pegar en clave del agente Hola copiado de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9bee6-185">In hello **Sync Metadata Database Configuration** dialog box, paste in hello agent key copied from hello Azure portal.</span></span> <span data-ttu-id="9bee6-186">También se proporcionan credenciales existentes de hello para el servidor de base de datos de SQL Azure de hello en qué Hola se encuentra la base de datos de metadatos.</span><span class="sxs-lookup"><span data-stu-id="9bee6-186">Also provide hello existing credentials for hello Azure SQL Database server on which hello metadata database is located.</span></span> <span data-ttu-id="9bee6-187">(Si ha creado una nueva base de datos de metadatos, esta base de datos está en hello mismo servidor que la base de datos de base de datos central de Hola.) Seleccione **Aceptar** y espere Hola configuración toofinish.</span><span class="sxs-lookup"><span data-stu-id="9bee6-187">(If you created a new metadata database, this database is on hello same server as hello hub database.) Select **OK** and wait for hello configuration toofinish.</span></span>

        ![Escriba las credenciales de clave y el servidor de agente Hola](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-enterkey.png)

        >   [!NOTE] 
        >   <span data-ttu-id="9bee6-189">Si recibe un error de firewall en este momento, tener una toocreate una regla de firewall en Azure tooallow el tráfico entrante del equipo de SQL Server de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bee6-189">If you get a firewall error at this point, you have toocreate a firewall rule on Azure tooallow incoming traffic from hello SQL Server computer.</span></span> <span data-ttu-id="9bee6-190">Puede crear reglas de hello manualmente en el portal de hello, pero quizá le resulte más fácil toocreate que en SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="9bee6-190">You can create hello rule manually in hello portal, but you may find it easier toocreate it in SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="9bee6-191">En SSMS, pruebe a base de datos de tooconnect toohello central en Azure.</span><span class="sxs-lookup"><span data-stu-id="9bee6-191">In SSMS, try tooconnect toohello hub database on Azure.</span></span> <span data-ttu-id="9bee6-192">Escriba su nombre como \<hub_database_name\>.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="9bee6-192">Enter its name as \<hub_database_name\>.database.windows.net.</span></span> <span data-ttu-id="9bee6-193">Siga los pasos de Hola de regla de firewall de Azure de Hola de tooconfigure cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bee6-193">Follow hello steps in hello dialog box tooconfigure hello Azure firewall rule.</span></span> <span data-ttu-id="9bee6-194">A continuación, devolver toohello aplicación de agente de sincronización cliente.</span><span class="sxs-lookup"><span data-stu-id="9bee6-194">Then return toohello Client Sync Agent app.</span></span>

    9.  <span data-ttu-id="9bee6-195">En la aplicación del agente de sincronización cliente hello, haga clic en **registrar** tooregister una base de datos de SQL Server con el agente de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bee6-195">In hello Client Sync Agent app, click **Register** tooregister a SQL Server database with hello agent.</span></span> <span data-ttu-id="9bee6-196">Hola **configuración de SQL Server** abre el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9bee6-196">hello **SQL Server Configuration** dialog box opens.</span></span>

        ![Adición y configuración de una instancia de SQL Server Database](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-adddb.png)

    10. <span data-ttu-id="9bee6-198">Hola **configuración de SQL Server** diálogo cuadro, elija si tooconnect mediante autenticación de SQL Server o autenticación de Windows.</span><span class="sxs-lookup"><span data-stu-id="9bee6-198">In hello **SQL Server Configuration** dialog box, choose whether tooconnect by using SQL Server authentication or Windows authentication.</span></span> <span data-ttu-id="9bee6-199">Si elige la autenticación de SQL Server, escriba las credenciales existentes de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bee6-199">If you chose SQL Server authentication, enter hello existing credentials.</span></span> <span data-ttu-id="9bee6-200">Proporcione nombre de SQL Server de Hola y Hola de base de datos de Hola que desea toosync.</span><span class="sxs-lookup"><span data-stu-id="9bee6-200">Provide hello SQL Server name and hello name of hello database that you want toosync.</span></span> <span data-ttu-id="9bee6-201">Seleccione **Probar conexión** tootest la configuración.</span><span class="sxs-lookup"><span data-stu-id="9bee6-201">Select **Test connection** tootest your settings.</span></span> <span data-ttu-id="9bee6-202">Después, seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="9bee6-202">Then select **Save**.</span></span> <span data-ttu-id="9bee6-203">base de datos registrada de Hola aparece en la lista Hola.</span><span class="sxs-lookup"><span data-stu-id="9bee6-203">hello registered database appears in hello list.</span></span>

        ![La base de datos de SQL Server ya está registrada](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-dbadded.png)

    11. <span data-ttu-id="9bee6-205">Ahora puede cerrar la aplicación del agente de sincronización cliente hello.</span><span class="sxs-lookup"><span data-stu-id="9bee6-205">You can now close hello Client Sync Agent app.</span></span>

    12. <span data-ttu-id="9bee6-206">En el portal de hello, en hello **configurar On-Premises** hoja, seleccione **seleccione Hola base de datos.**</span><span class="sxs-lookup"><span data-stu-id="9bee6-206">In hello portal, on hello **Configure On-Premises** blade, select **Select hello Database.**</span></span> <span data-ttu-id="9bee6-207">Hola **Seleccionar base de datos** abre la hoja.</span><span class="sxs-lookup"><span data-stu-id="9bee6-207">hello **Select Database** blade opens.</span></span>

    13. <span data-ttu-id="9bee6-208">En hello **Seleccionar base de datos** hoja en hello **nombre del miembro de sincronización** campo, proporcione un nombre para el nuevo miembro de sincronización Hola.</span><span class="sxs-lookup"><span data-stu-id="9bee6-208">On hello **Select Database** blade, in hello **Sync Member Name** field, provide a name for hello new sync member.</span></span> <span data-ttu-id="9bee6-209">Este nombre es distinto del nombre de Hola de hello propia base de datos.</span><span class="sxs-lookup"><span data-stu-id="9bee6-209">This name is distinct from hello name of hello database itself.</span></span> <span data-ttu-id="9bee6-210">Seleccionar base de datos de hello lista Hola.</span><span class="sxs-lookup"><span data-stu-id="9bee6-210">Select hello database from hello list.</span></span> <span data-ttu-id="9bee6-211">Hola **direcciones de sincronización** , a continuación, seleccionar la sincronización bidireccional, toohello concentrador, o de hello concentrador.</span><span class="sxs-lookup"><span data-stu-id="9bee6-211">In hello **Sync Directions** field, select Bi-directional Sync, toohello Hub, or From hello Hub.</span></span>

        ![Seleccione hello en la base de datos local](media/sql-database-get-started-sql-data-sync/datasync-preview-selectdb.png)

    14. <span data-ttu-id="9bee6-213">Seleccione **Aceptar** tooclose hello **Seleccionar base de datos** hoja.</span><span class="sxs-lookup"><span data-stu-id="9bee6-213">Select **OK** tooclose hello **Select Database** blade.</span></span> <span data-ttu-id="9bee6-214">A continuación, seleccione **Aceptar** tooclose hello **configurar local** hoja y espere a que Hola sincronizan nuevos miembros toobe creado e implementado.</span><span class="sxs-lookup"><span data-stu-id="9bee6-214">Then select **OK** tooclose hello **Configure On-Premises** blade and wait for hello new sync member toobe created and deployed.</span></span> <span data-ttu-id="9bee6-215">Por último, haga clic en **Aceptar** tooclose hello **seleccionar miembros de sincronización** hoja.</span><span class="sxs-lookup"><span data-stu-id="9bee6-215">Finally, click **OK** tooclose hello **Select sync members** blade.</span></span>

        ![En la base de datos local se ha agregado toosync grupo](media/sql-database-get-started-sql-data-sync/datasync-preview-onpremadded.png)

3.  <span data-ttu-id="9bee6-217">tooconnect tooSQL Data Sync y el agente local de hello, agregar el rol de toohello de nombre de usuario `DataSync_Executor`.</span><span class="sxs-lookup"><span data-stu-id="9bee6-217">tooconnect tooSQL Data Sync and hello local agent, add your user name toohello role `DataSync_Executor`.</span></span> <span data-ttu-id="9bee6-218">Sincronización de datos, crea este rol en la instancia de SQL Server de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bee6-218">Data Sync creates this role on hello SQL Server instance.</span></span>

## <a name="step-3---configure-sync-group"></a><span data-ttu-id="9bee6-219">Paso 3: Configuración del grupo de sincronización</span><span class="sxs-lookup"><span data-stu-id="9bee6-219">Step 3 - Configure sync group</span></span>

<span data-ttu-id="9bee6-220">Una vez creados e implementados, paso 3, miembros del grupo de sincronización nuevo de hello **Configurar grupo de sincronización**, se resalta en hello **nuevo grupo de sincronización** hoja.</span><span class="sxs-lookup"><span data-stu-id="9bee6-220">After hello new sync group members are created and deployed, Step 3, **Configure sync group**, is highlighted in hello **New sync group** blade.</span></span>

1.  <span data-ttu-id="9bee6-221">En hello **tablas** hoja, seleccione una base de datos de lista de Hola de sincronización de miembros del grupo y, a continuación, seleccione **actualizar esquema**.</span><span class="sxs-lookup"><span data-stu-id="9bee6-221">On hello **Tables** blade, select a database from hello list of sync group members, and then select **Refresh schema**.</span></span>

2.  <span data-ttu-id="9bee6-222">En lista de Hola de tablas disponibles, seleccione las tablas de Hola que desea toosync.</span><span class="sxs-lookup"><span data-stu-id="9bee6-222">From hello list of available tables, select hello tables that you want toosync.</span></span>

    ![Seleccionar las tablas toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-tables.png)

3.  <span data-ttu-id="9bee6-224">De forma predeterminada, se seleccionan todas las columnas de tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bee6-224">By default, all columns in hello table are selected.</span></span> <span data-ttu-id="9bee6-225">Si no desea toosync todas las columnas de hello, deshabilite Hola casilla de verificación para las columnas de Hola que no desea toosync.</span><span class="sxs-lookup"><span data-stu-id="9bee6-225">If you don't want toosync all hello columns, disable hello checkbox for hello columns that you don't want toosync.</span></span> <span data-ttu-id="9bee6-226">Asegúrese de selecciona columna de clave principal de tooleave Hola.</span><span class="sxs-lookup"><span data-stu-id="9bee6-226">Be sure tooleave hello primary key column selected.</span></span>

    ![Seleccionar campos toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-tables2.png)

4.  <span data-ttu-id="9bee6-228">Por último, seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="9bee6-228">Finally, select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9bee6-229">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9bee6-229">Next steps</span></span>
<span data-ttu-id="9bee6-230">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="9bee6-230">Congratulations.</span></span> <span data-ttu-id="9bee6-231">Ha creado un grupo de sincronización que incluye una instancia de SQL Database y una base de datos de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9bee6-231">You have created a sync group that includes both a SQL Database instance and a SQL Server database.</span></span>

<span data-ttu-id="9bee6-232">Para obtener más información sobre SQL Database y SQL Data Sync, vea:</span><span class="sxs-lookup"><span data-stu-id="9bee6-232">For more info about SQL Database and SQL Data Sync, see:</span></span>

-   [<span data-ttu-id="9bee6-233">Descargar documentación técnica de hello completa de SQL Data Sync</span><span class="sxs-lookup"><span data-stu-id="9bee6-233">Download hello complete SQL Data Sync technical documentation</span></span>](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)
-   [<span data-ttu-id="9bee6-234">Descargue la documentación de API de REST de sincronización de datos de SQL de Hola</span><span class="sxs-lookup"><span data-stu-id="9bee6-234">Download hello SQL Data Sync REST API documentation</span></span>](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)
-   [<span data-ttu-id="9bee6-235">Información general de SQL Database</span><span class="sxs-lookup"><span data-stu-id="9bee6-235">SQL Database Overview</span></span>](sql-database-technical-overview.md)
-   [<span data-ttu-id="9bee6-236">Administración del ciclo de vida de las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="9bee6-236">Database Lifecycle Management</span></span>](https://msdn.microsoft.com/library/jj907294.aspx)
