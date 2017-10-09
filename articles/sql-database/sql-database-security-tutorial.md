---
title: aaaSecure la base de datos SQL de Azure | Documentos de Microsoft
description: "Obtenga información sobre características y técnicas de toosecure la base de datos de SQL Azure."
services: sql-database
documentationcenter: 
author: DRediske
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/28/2017
ms.author: daredis
ms.openlocfilehash: 1450d633d6f65faf1b8a2dc0dc7dfe996fb0719d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="secure-your-azure-sql-database"></a><span data-ttu-id="ecc00-103">Protección de Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="ecc00-103">Secure your Azure SQL Database</span></span>

<span data-ttu-id="ecc00-104">Base de datos SQL protege los datos mediante la limitación de base de datos de access tooyour mediante las reglas de firewall que requieren los usuarios tooprove su identidad y autorización toodata a través de pertenencia basada en roles y permisos, así como a través de mecanismos de autenticación seguridad de nivel de fila y enmascaramiento dinámico de datos.</span><span class="sxs-lookup"><span data-stu-id="ecc00-104">SQL Database secures your data by limiting access tooyour database using firewall rules, authentication mechanisms requiring users tooprove their identity, and authorization toodata through role-based memberships and permissions, as well as through row-level security and dynamic data masking.</span></span>

<span data-ttu-id="ecc00-105">Puede mejorar la protección de hello de la base de datos frente a accesos no autorizados con unos pocos pasos sencillos o usuarios malintencionados.</span><span class="sxs-lookup"><span data-stu-id="ecc00-105">You can improve hello protection of your database against malicious users or unauthorized access with just a few simple steps.</span></span> <span data-ttu-id="ecc00-106">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="ecc00-106">In this tutorial you learn to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="ecc00-107">Configurar reglas de firewall de nivel de servidor para el servidor en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="ecc00-107">Set up server-level firewall rules for your server in hello Azure portal</span></span>
> * <span data-ttu-id="ecc00-108">Configurar reglas de firewall de nivel de base de datos para la base de datos con SSMS</span><span class="sxs-lookup"><span data-stu-id="ecc00-108">Set up database-level firewall rules for your database using SSMS</span></span>
> * <span data-ttu-id="ecc00-109">Conéctese utilizando una cadena de conexión segura de base de datos de tooyour</span><span class="sxs-lookup"><span data-stu-id="ecc00-109">Connect tooyour database using a secure connection string</span></span>
> * <span data-ttu-id="ecc00-110">Administrar el acceso de los usuarios</span><span class="sxs-lookup"><span data-stu-id="ecc00-110">Manage user access</span></span>
> * <span data-ttu-id="ecc00-111">Protección de los datos con cifrado</span><span class="sxs-lookup"><span data-stu-id="ecc00-111">Protect your data with encryption</span></span>
> * <span data-ttu-id="ecc00-112">Habilitación de la auditoría de SQL Database</span><span class="sxs-lookup"><span data-stu-id="ecc00-112">Enable SQL Database auditing</span></span>
> * <span data-ttu-id="ecc00-113">Habilitación de la detección de amenazas de SQL Database</span><span class="sxs-lookup"><span data-stu-id="ecc00-113">Enable SQL Database threat detection</span></span>

<span data-ttu-id="ecc00-114">Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="ecc00-114">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ecc00-115">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ecc00-115">Prerequisites</span></span>

<span data-ttu-id="ecc00-116">toocomplete Asegúrese de este tutorial, deberá asegurarse de que Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="ecc00-116">toocomplete this tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="ecc00-117">Versión más reciente de hello instalada de [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="ecc00-117">Installed hello newest version of [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span></span> 
- <span data-ttu-id="ecc00-118">Se ha instalado Microsoft Excel</span><span class="sxs-lookup"><span data-stu-id="ecc00-118">Installed Microsoft Excel</span></span>
- <span data-ttu-id="ecc00-119">Crea un servidor de SQL Azure y la base de datos: vea [crear una base de datos de SQL Azure en el portal de Azure hello](sql-database-get-started-portal.md), [crear una base de datos de SQL Azure único con hello Azure CLI](sql-database-get-started-cli.md), y [crear una instancia única de SQL Azure uso de PowerShell de la base de datos](sql-database-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="ecc00-119">Created an Azure SQL server and database - See [Create an Azure SQL database in hello Azure portal](sql-database-get-started-portal.md), [Create a single Azure SQL database using hello Azure CLI](sql-database-get-started-cli.md), and [Create a single Azure SQL database using PowerShell](sql-database-get-started-powershell.md).</span></span> 

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="ecc00-120">Inicie sesión en toohello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="ecc00-120">Log in toohello Azure portal</span></span>

<span data-ttu-id="ecc00-121">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ecc00-121">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="ecc00-122">Crear una regla de firewall de nivel de servidor en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="ecc00-122">Create a server-level firewall rule in hello Azure portal</span></span>

<span data-ttu-id="ecc00-123">En Azure, las bases de datos SQL están protegidas mediante un firewall.</span><span class="sxs-lookup"><span data-stu-id="ecc00-123">SQL databases are protected by a firewall in Azure.</span></span> <span data-ttu-id="ecc00-124">De forma predeterminada, se rechazan todas las conexiones toohello hello y servidor de bases de datos dentro de servidor hello excepto para las conexiones desde otros servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="ecc00-124">By default, all connections toohello server and hello databases inside hello server are rejected except for connections from other Azure services.</span></span> <span data-ttu-id="ecc00-125">Para más información, consulte [Reglas de firewall de nivel de base de datos y de nivel de servidor de Azure SQL Database](sql-database-firewall-configure.md).</span><span class="sxs-lookup"><span data-stu-id="ecc00-125">For more information, see [Azure SQL Database server-level and database-level firewall rules](sql-database-firewall-configure.md).</span></span>

<span data-ttu-id="ecc00-126">configuración más segura de Hello es tooset 'Permitir acceso a servicios tooAzure' tooOFF.</span><span class="sxs-lookup"><span data-stu-id="ecc00-126">hello most secure configuration is tooset 'Allow access tooAzure services' tooOFF.</span></span> <span data-ttu-id="ecc00-127">Si necesita tooconnect toohello base de datos de un servicio de máquina virtual de Azure o en la nube, debe crear un [IP reservada](../virtual-network/virtual-networks-reserved-public-ip.md) y permitir solo Hola reservado IP abordar el acceso a través de firewall de Hola.</span><span class="sxs-lookup"><span data-stu-id="ecc00-127">If you need tooconnect toohello database from an Azure VM or cloud service, you should create a [Reserved IP](../virtual-network/virtual-networks-reserved-public-ip.md) and allow only hello reserved IP address access through hello firewall.</span></span> 

<span data-ttu-id="ecc00-128">Siga estos pasos toocreate una [regla de firewall de nivel de servidor de base de datos SQL](sql-database-firewall-configure.md) para las conexiones del servidor tooallow desde una dirección IP específica.</span><span class="sxs-lookup"><span data-stu-id="ecc00-128">Follow these steps toocreate a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your server tooallow connections from a specific IP address.</span></span> 

> [!NOTE]
> <span data-ttu-id="ecc00-129">Si ha creado una base de datos de ejemplo en Azure mediante uno de los tutoriales anteriores de Hola o tutoriales rápidos y están realizando este tutorial en un equipo con hello mismo de direcciones IP que TI tenía cuando le guía por los tutoriales, puede omitir este paso ya que tendrá ya creó una regla de firewall de nivel de servidor.</span><span class="sxs-lookup"><span data-stu-id="ecc00-129">If you have created a sample database in Azure using one of hello previous tutorials or quickstarts and are performing this tutorial on a computer with hello same IP address that it had when you walked through those tutorials, you can skip this step as you will have already created a server-level firewall rule.</span></span>
>

1. <span data-ttu-id="ecc00-130">Haga clic en **bases de datos SQL** de hello izquierdo menú y haga clic en hello base de datos desearía tooconfigure regla de firewall de Hola para en hello **bases de datos SQL** página.</span><span class="sxs-lookup"><span data-stu-id="ecc00-130">Click **SQL databases** from hello left-hand menu and click hello database you would like tooconfigure hello firewall rule for on hello **SQL databases** page.</span></span> <span data-ttu-id="ecc00-131">página de información general para abrir el base de datos, que muestra que Hola totalmente Hello calificado nombre del servidor (como **mynewserver 20170313.database.windows.net**) y proporciona opciones para otra configuración.</span><span class="sxs-lookup"><span data-stu-id="ecc00-131">hello overview page for your database opens, showing you hello fully qualified server name (such as **mynewserver-20170313.database.windows.net**) and provides options for further configuration.</span></span>

      ![regla de firewall del servidor](./media/sql-database-security-tutorial/server-firewall-rule.png) 

2. <span data-ttu-id="ecc00-133">Haga clic en **Configurar firewall de servidor** de barra de herramientas de hello tal y como se muestra en la imagen anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="ecc00-133">Click **Set server firewall** on hello toolbar as shown in hello previous image.</span></span> <span data-ttu-id="ecc00-134">Hola **configuración del Firewall** se abre la página servidor de base de datos de SQL de Hola.</span><span class="sxs-lookup"><span data-stu-id="ecc00-134">hello **Firewall settings** page for hello SQL Database server opens.</span></span> 

3. <span data-ttu-id="ecc00-135">Haga clic en **agregar dirección IP del cliente** en Hola barra de herramientas tooadd Hola dirección IP pública del portal de hello equipo toohello conectado con o escribir la regla de firewall de hello manualmente y, a continuación, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="ecc00-135">Click **Add client IP** on hello toolbar tooadd hello public IP address of hello computer connected toohello portal with or enter hello firewall rule manually and then click **Save**.</span></span>

      ![establecer regla de firewall del servidor](./media/sql-database-security-tutorial/server-firewall-rule-set.png) 

4. <span data-ttu-id="ecc00-137">Haga clic en **Aceptar** y, a continuación, haga clic en hello **X** tooclose hello **configuración del Firewall** página.</span><span class="sxs-lookup"><span data-stu-id="ecc00-137">Click **OK** and then click hello **X** tooclose hello **Firewall settings** page.</span></span>

<span data-ttu-id="ecc00-138">Ahora puede conectarse tooany base de datos en el servidor de hello con hello especificado intervalo de direcciones IP o la dirección IP.</span><span class="sxs-lookup"><span data-stu-id="ecc00-138">You can now connect tooany database in hello server with hello specified IP address or IP address range.</span></span>

> [!NOTE]
> <span data-ttu-id="ecc00-139">SQL Database se comunica a través del puerto 1433.</span><span class="sxs-lookup"><span data-stu-id="ecc00-139">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="ecc00-140">Si está tratando de tooconnect desde dentro de una red corporativa, es posible que firewall de su red no permite el tráfico saliente en el puerto 1433.</span><span class="sxs-lookup"><span data-stu-id="ecc00-140">If you are trying tooconnect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="ecc00-141">Si es así, no será capaz de tooconnect tooyour base de datos de SQL Azure servidor a menos que el departamento de TI abre el puerto 1433.</span><span class="sxs-lookup"><span data-stu-id="ecc00-141">If so, you will not be able tooconnect tooyour Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-level-firewall-rule-using-ssms"></a><span data-ttu-id="ecc00-142">Creación de una regla de firewall de nivel de base de datos con SSMS</span><span class="sxs-lookup"><span data-stu-id="ecc00-142">Create a database-level firewall rule using SSMS</span></span>

<span data-ttu-id="ecc00-143">Las reglas de firewall de nivel de base de datos Habilitar configuración de otro firewall toocreate para bases de datos diferentes dentro de hello mismo firewall de servidor y toocreate lógico reglas que sean portables - lo que significa que se adecuan a base de datos de Hola durante un [conmutación por error ](sql-database-geo-replication-overview.md) en lugar de almacenarse en SQL server de Hola.</span><span class="sxs-lookup"><span data-stu-id="ecc00-143">Database-level firewall rules enable you toocreate different firewall settings for different databases within hello same logical server and toocreate firewall rules that are portable - meaning that they follow hello database during a [failover](sql-database-geo-replication-overview.md) rather than being stored on hello SQL server.</span></span> <span data-ttu-id="ecc00-144">Reglas de firewall de nivel de base de datos solo se pueden configurar mediante el uso de instrucciones Transact-SQL como solo después de haber configurado la primera regla de firewall de nivel de servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="ecc00-144">Database-level firewall rules can only be configured by using Transact-SQL statements and only after you have configured hello first server-level firewall rule.</span></span> <span data-ttu-id="ecc00-145">Para más información, consulte [Reglas de firewall de nivel de base de datos y de nivel de servidor de Azure SQL Database](sql-database-firewall-configure.md).</span><span class="sxs-lookup"><span data-stu-id="ecc00-145">For more information, see [Azure SQL Database server-level and database-level firewall rules](sql-database-firewall-configure.md).</span></span>

<span data-ttu-id="ecc00-146">Sigue estos toocreate pasos una regla de firewall de base de datos específica.</span><span class="sxs-lookup"><span data-stu-id="ecc00-146">Follows these steps toocreate a database-specific firewall rule.</span></span>

1. <span data-ttu-id="ecc00-147">Conectar la base de datos de tooyour, por ejemplo mediante [SQL Server Management Studio](./sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="ecc00-147">Connect tooyour database, for example using [SQL Server Management Studio](./sql-database-connect-query-ssms.md).</span></span>

2. <span data-ttu-id="ecc00-148">En el Explorador de objetos, haga doble clic en la base de datos de hello desea tooadd un firewall para de la regla y haga clic en **nueva consulta**.</span><span class="sxs-lookup"><span data-stu-id="ecc00-148">In Object Explorer, right-click on hello database you want tooadd a firewall rule for and click **New Query**.</span></span> <span data-ttu-id="ecc00-149">Abre una ventana de consulta en blanco que es conectado tooyour base de datos.</span><span class="sxs-lookup"><span data-stu-id="ecc00-149">A blank query window opens that is connected tooyour database.</span></span>

3. <span data-ttu-id="ecc00-150">En la ventana de consulta de hello, modifique hello tooyour pública dirección IP y, a continuación, ejecute hello después de consulta:</span><span class="sxs-lookup"><span data-stu-id="ecc00-150">In hello query window, modify hello IP address tooyour public IP address and then execute hello following query:</span></span>

    ```sql
    EXECUTE sp_set_database_firewall_rule N'Example DB Rule','0.0.0.4','0.0.0.4';
    ```

4. <span data-ttu-id="ecc00-151">En la barra de herramientas de hello, haga clic en **Execute** regla de firewall toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="ecc00-151">On hello toolbar, click **Execute** toocreate hello firewall rule.</span></span>

## <a name="view-how-tooconnect-an-application-tooyour-database-using-a-secure-connection-string"></a><span data-ttu-id="ecc00-152">Ver cómo tooconnect tooyour de una aplicación de base de datos mediante una cadena de conexión segura</span><span class="sxs-lookup"><span data-stu-id="ecc00-152">View how tooconnect an application tooyour database using a secure connection string</span></span>

<span data-ttu-id="ecc00-153">tooensure una conexión cifrada segura entre una aplicación cliente y la base de datos SQL, cadena de conexión de hello tiene toobe configurado para:</span><span class="sxs-lookup"><span data-stu-id="ecc00-153">tooensure a secure, encrypted connection between a client application and SQL Database, hello connection string has toobe configured to:</span></span>

- <span data-ttu-id="ecc00-154">Solicitar una conexión cifrada y</span><span class="sxs-lookup"><span data-stu-id="ecc00-154">Request an encrypted connection, and</span></span>
- <span data-ttu-id="ecc00-155">certificado de servidor de toonot confianza Hola.</span><span class="sxs-lookup"><span data-stu-id="ecc00-155">toonot trust hello server certificate.</span></span> 

<span data-ttu-id="ecc00-156">Esto establece una conexión con seguridad de capa de transporte (TLS) y reduce el riesgo de Hola de man-in-the-middle ataques.</span><span class="sxs-lookup"><span data-stu-id="ecc00-156">This establishes a connection using Transport Layer Security (TLS) and reduces hello risk of man-in-the-middle attacks.</span></span> <span data-ttu-id="ecc00-157">Puede obtener las cadenas de conexión configurada correctamente para la base de datos SQL de cliente admitida controladores de hello portal de Azure como se muestra para ADO.net en esta captura de pantalla.</span><span class="sxs-lookup"><span data-stu-id="ecc00-157">You can obtain correctly configured connection strings for your SQL Database for supported client drivers from hello Azure portal as shown for ADO.net in this screenshot.</span></span>

1. <span data-ttu-id="ecc00-158">Seleccione **bases de datos SQL** desde el menú de la izquierda, hello y haga clic en la base de datos en hello **bases de datos SQL** página.</span><span class="sxs-lookup"><span data-stu-id="ecc00-158">Select **SQL databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span>

2. <span data-ttu-id="ecc00-159">En hello **Introducción** página de la base de datos, haga clic en **mostrar cadenas de conexión de base de datos**.</span><span class="sxs-lookup"><span data-stu-id="ecc00-159">On hello **Overview** page for your database, click **Show database connection strings**.</span></span>

3. <span data-ttu-id="ecc00-160">Hola de revisión completa **ADO.NET** cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="ecc00-160">Review hello complete **ADO.NET** connection string.</span></span>

    ![Cadena de conexión ADO.NET](./media/sql-database-security-tutorial/adonet-connection-string.png)

## <a name="creating-database-users"></a><span data-ttu-id="ecc00-162">Creación de usuarios de base de datos</span><span class="sxs-lookup"><span data-stu-id="ecc00-162">Creating database users</span></span>

<span data-ttu-id="ecc00-163">Antes de crear los usuarios, primero debe elegir uno de dos tipos de autenticación admitidos por Azure SQL Database:</span><span class="sxs-lookup"><span data-stu-id="ecc00-163">Before creating any users, you must first choose from one of two authentication types supported by Azure SQL Database:</span></span> 

<span data-ttu-id="ecc00-164">**Autenticación de SQL**, que utiliza el nombre de usuario y contraseña para los inicios de sesión y Hola a los usuarios que son válidos únicamente en el contexto de una base de datos dentro de un servidor lógico.</span><span class="sxs-lookup"><span data-stu-id="ecc00-164">**SQL Authentication**, which uses username and password for logins and users that are valid only in hello context of a specific database within a logical server.</span></span> 

<span data-ttu-id="ecc00-165">**Autenticación de Azure Active Directory**, que usa identidades administradas por Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ecc00-165">**Azure Active Directory Authentication**, which uses identities managed by Azure Active Directory.</span></span> 

<span data-ttu-id="ecc00-166">Si desea que toouse [Azure Active Directory](./sql-database-aad-authentication.md) tooauthenticate en base de datos de SQL, debe existir un rellenado Azure Active Directory antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="ecc00-166">If you want toouse [Azure Active Directory](./sql-database-aad-authentication.md) tooauthenticate against SQL Database, a populated Azure Active Directory must exist before you can proceed.</span></span>

<span data-ttu-id="ecc00-167">Siga estos pasos toocreate un usuario mediante la autenticación de SQL:</span><span class="sxs-lookup"><span data-stu-id="ecc00-167">Follow these steps toocreate a user using SQL Authentication:</span></span>

1. <span data-ttu-id="ecc00-168">Conectar la base de datos de tooyour, por ejemplo mediante [SQL Server Management Studio](./sql-database-connect-query-ssms.md) con sus credenciales de administrador de servidor.</span><span class="sxs-lookup"><span data-stu-id="ecc00-168">Connect tooyour database, for example using [SQL Server Management Studio](./sql-database-connect-query-ssms.md) using your server admin credentials.</span></span>

2. <span data-ttu-id="ecc00-169">En el Explorador de objetos, haga doble clic en la base de datos de Hola que desee tooadd un usuario nuevo y haga clic en **nueva consulta**.</span><span class="sxs-lookup"><span data-stu-id="ecc00-169">In Object Explorer, right-click on hello database you want tooadd a new user on and click **New Query**.</span></span> <span data-ttu-id="ecc00-170">Abre una ventana de consulta en blanco que es toohello conectado la base de datos seleccionada.</span><span class="sxs-lookup"><span data-stu-id="ecc00-170">A blank query window opens that is connected toohello selected database.</span></span>

3. <span data-ttu-id="ecc00-171">En la ventana de consulta de hello, escriba Hola después de consulta:</span><span class="sxs-lookup"><span data-stu-id="ecc00-171">In hello query window, enter hello following query:</span></span>

    ```sql
    CREATE USER ApplicationUser WITH PASSWORD = 'YourStrongPassword1';
    ```

4. <span data-ttu-id="ecc00-172">En la barra de herramientas de hello, haga clic en **Execute** toocreate usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="ecc00-172">On hello toolbar, click **Execute** toocreate hello user.</span></span>

5. <span data-ttu-id="ecc00-173">De forma predeterminada, usuario de hello puede conectar la base de datos de toohello, pero no tiene ningún dato de tooread o de escritura de permisos.</span><span class="sxs-lookup"><span data-stu-id="ecc00-173">By default, hello user can connect toohello database, but has no permissions tooread or write data.</span></span> <span data-ttu-id="ecc00-174">toogrant estas toohello permisos usuario creado recientemente, ejecute hello siguiendo dos comandos en una nueva ventana de consulta</span><span class="sxs-lookup"><span data-stu-id="ecc00-174">toogrant these permissions toohello newly created user, execute hello following two commands in a new query window</span></span>

    ```sql
    ALTER ROLE db_datareader ADD MEMBER ApplicationUser;
    ALTER ROLE db_datawriter ADD MEMBER ApplicationUser;
    ```

<span data-ttu-id="ecc00-175">Es mejor toocreate práctica estas cuentas sin privilegios de administrador en tooyour de tooconnect de nivel de base de datos de Hola de base de datos a menos que necesite tooexecute tareas de administrador como la creación de nuevos usuarios.</span><span class="sxs-lookup"><span data-stu-id="ecc00-175">It is best practice toocreate these non-administrator accounts at hello database level tooconnect tooyour database unless you need tooexecute administrator tasks like creating new users.</span></span> <span data-ttu-id="ecc00-176">Revise hello [tutorial de Azure Active Directory](./sql-database-aad-authentication-configure.md) acerca de cómo tooauthenticate con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ecc00-176">Please review hello [Azure Active Directory tutorial](./sql-database-aad-authentication-configure.md) on how tooauthenticate using Azure Active Directory.</span></span>


## <a name="protect-your-data-with-encryption"></a><span data-ttu-id="ecc00-177">Protección de los datos con cifrado</span><span class="sxs-lookup"><span data-stu-id="ecc00-177">Protect your data with encryption</span></span>

<span data-ttu-id="ecc00-178">Cifrado de datos transparente de base de datos de SQL Azure (TDE) cifra automáticamente los datos en reposo, sin necesidad de realizar los cambios toohello aplicación acceso a Hola base de datos cifrada.</span><span class="sxs-lookup"><span data-stu-id="ecc00-178">Azure SQL Database transparent data encryption (TDE) automatically encrypts your data at rest, without requiring any changes toohello application accessing hello encrypted database.</span></span> <span data-ttu-id="ecc00-179">Para las bases de datos recién creadas, el TDE está activado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="ecc00-179">For newly created databases, TDE is on by default.</span></span> <span data-ttu-id="ecc00-180">tooenable TDE para su base de datos o tooverify que TDE está activado, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="ecc00-180">tooenable TDE for your database or tooverify that TDE is on, follow these steps:</span></span>

1. <span data-ttu-id="ecc00-181">Seleccione **bases de datos SQL** desde el menú de la izquierda, hello y haga clic en la base de datos en hello **bases de datos SQL** página.</span><span class="sxs-lookup"><span data-stu-id="ecc00-181">Select **SQL databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 

2. <span data-ttu-id="ecc00-182">Haga clic en **cifrado de datos transparente** página de configuración de hello tooopen de TDE.</span><span class="sxs-lookup"><span data-stu-id="ecc00-182">Click on **Transparent data encryption** tooopen hello configuration page for TDE.</span></span>

    ![Cifrado de datos transparente](./media/sql-database-security-tutorial/transparent-data-encryption-enabled.png)

3. <span data-ttu-id="ecc00-184">Si es necesario, establezca **cifrado de datos** tooON y haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="ecc00-184">If necessary, set **Data encryption** tooON and click **Save**.</span></span>

<span data-ttu-id="ecc00-185">se inicia el proceso de cifrado de Hello en segundo plano de Hola.</span><span class="sxs-lookup"><span data-stu-id="ecc00-185">hello encryption process starts in hello background.</span></span> <span data-ttu-id="ecc00-186">Puede supervisar el progreso de hello usando conexión de base de datos de tooSQL [SQL Server Management Studio](./sql-database-connect-query-ssms.md) consultando la columna encryption_state de Hola de hello `sys.dm_database_encryption_keys` vista.</span><span class="sxs-lookup"><span data-stu-id="ecc00-186">You can monitor hello progress by connecting tooSQL Database using [SQL Server Management Studio](./sql-database-connect-query-ssms.md) by querying hello encryption_state column of hello `sys.dm_database_encryption_keys` view.</span></span>

## <a name="enable-sql-database-auditing-if-necessary"></a><span data-ttu-id="ecc00-187">Habilitación de la auditoría de SQL Database, si es necesario</span><span class="sxs-lookup"><span data-stu-id="ecc00-187">Enable SQL Database auditing, if necessary</span></span>

<span data-ttu-id="ecc00-188">Auditoría de base de datos de SQL Azure realiza un seguimiento de eventos de base de datos y escribe el registro de auditoría tooan en su cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="ecc00-188">Azure SQL Database Auditing tracks database events and writes them tooan audit log in your Azure Storage account.</span></span> <span data-ttu-id="ecc00-189">La auditoría puede ayudarle a mantener el cumplimiento de normativas y conocer la actividad de las bases de datos, así como las discrepancias y anomalías que pueden indicar la existencia de potenciales infracciones de la seguridad.</span><span class="sxs-lookup"><span data-stu-id="ecc00-189">Auditing can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate potential security violations.</span></span> <span data-ttu-id="ecc00-190">Siga estos toocreate pasos una directiva de auditoría predeterminada para la base de datos SQL:</span><span class="sxs-lookup"><span data-stu-id="ecc00-190">Follow these steps toocreate a default auditing policy for your SQL database:</span></span>

1. <span data-ttu-id="ecc00-191">Seleccione **bases de datos SQL** desde el menú de la izquierda, hello y haga clic en la base de datos en hello **bases de datos SQL** página.</span><span class="sxs-lookup"><span data-stu-id="ecc00-191">Select **SQL databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 

2. <span data-ttu-id="ecc00-192">En la hoja de configuración de hello, seleccione **auditoría y la detección de amenazas**.</span><span class="sxs-lookup"><span data-stu-id="ecc00-192">In hello Settings blade, select **Auditing & Threat Detection**.</span></span> <span data-ttu-id="ecc00-193">Observe que ha sido la auditoría de nivel de servidor y que hay un **ver configuración del servidor** vínculo que le permite tooview o modificar la configuración de auditoría de servidor hello en este contexto.</span><span class="sxs-lookup"><span data-stu-id="ecc00-193">Notice that sever-level auditing is diabled and that there is a **View server settings** link that allows you tooview or modify hello server auditing settings from this context.</span></span>

    ![Hoja Auditoría](./media/sql-database-security-tutorial/auditing-get-started-settings.png)

3. <span data-ttu-id="ecc00-195">Si lo prefiere tooenable un tipo de auditoría (o ubicación?) diferente de hello especificada en el nivel de servidor hello, activar **ON** auditoría y elija hello **Blob** tipo de auditoría.</span><span class="sxs-lookup"><span data-stu-id="ecc00-195">If you prefer tooenable an Audit type (or location?) different from hello one specified at hello server level, turn **ON** Auditing, and choose hello **Blob** Auditing Type.</span></span> <span data-ttu-id="ecc00-196">Si está habilitada la auditoría de servidor blobs, auditoría de base de datos configurada de hello existirá paralelo con la auditoría de Blob de servidor hello.</span><span class="sxs-lookup"><span data-stu-id="ecc00-196">If server Blob auditing is enabled, hello database configured audit will exist side by side with hello server Blob audit.</span></span>

    ![Activar la auditoría](./media/sql-database-security-tutorial/auditing-get-started-turn-on.png)

4. <span data-ttu-id="ecc00-198">Seleccione **detalles de almacenamiento** tooopen Hola hoja de almacenamiento de registros de auditoría.</span><span class="sxs-lookup"><span data-stu-id="ecc00-198">Select **Storage Details** tooopen hello Audit Logs Storage Blade.</span></span> <span data-ttu-id="ecc00-199">Cuenta de almacenamiento de Azure Hola seleccione donde se guardará los registros y período de retención de hello, se eliminarán los registros antiguos después qué hello, a continuación, haga clic en **Aceptar** final Hola.</span><span class="sxs-lookup"><span data-stu-id="ecc00-199">Select hello Azure storage account where logs will be saved, and hello retention period, after which hello old logs will be deleted, then click **OK** at hello bottom.</span></span> 

   > [!TIP]
   > <span data-ttu-id="ecc00-200">Use Hola misma cuenta de almacenamiento para todas las bases de datos auditados tooget hello máximo partido de auditoría de hello informa de plantillas.</span><span class="sxs-lookup"><span data-stu-id="ecc00-200">Use hello same storage account for all audited databases tooget hello most out of hello auditing reports templates.</span></span>
   > 

5. <span data-ttu-id="ecc00-201">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="ecc00-201">Click **Save**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ecc00-202">Si desea toocustomize Hola auditar eventos, puede hacerlo a través de PowerShell o API de REST - vea hello [automatización (PowerShell / API de REST)](sql-database-auditing.md#subheading-7) sección para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="ecc00-202">If you want toocustomize hello audited events, you can do this via PowerShell or REST API - see hello [Automation (PowerShell / REST API)](sql-database-auditing.md#subheading-7) section for more details.</span></span>
>

## <a name="enable-sql-database-threat-detection"></a><span data-ttu-id="ecc00-203">Habilitación de la detección de amenazas de SQL Database</span><span class="sxs-lookup"><span data-stu-id="ecc00-203">Enable SQL Database threat detection</span></span>

<span data-ttu-id="ecc00-204">La detección de amenazas proporciona una nueva capa de seguridad, lo cual permite toodetect de los clientes y responde a amenazas de toopotential cuando se producen al proporcionar alertas de seguridad en actividades anómalas.</span><span class="sxs-lookup"><span data-stu-id="ecc00-204">Threat Detection provides a new layer of security, which enables customers toodetect and respond toopotential threats as they occur by providing security alerts on anomalous activities.</span></span> <span data-ttu-id="ecc00-205">Los usuarios pueden explorar eventos sospechosos hello mediante toodetermine de auditoría de base de datos de SQL Server si producir un tooaccess de intento de infracción o vulnerabilidad de seguridad de datos en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ecc00-205">Users can explore hello suspicious events using SQL Database Auditing toodetermine if they result from an attempt tooaccess, breach or exploit data in hello database.</span></span> <span data-ttu-id="ecc00-206">La detección de amenazas resulta sencillo tooaddress posibles amenazas toohello base de datos sin necesidad de hello toobe un experto en seguridad o administrar sistemas de supervisión de seguridad avanzada.</span><span class="sxs-lookup"><span data-stu-id="ecc00-206">Threat Detection makes it simple tooaddress potential threats toohello database without hello need toobe a security expert or manage advanced security monitoring systems.</span></span>
<span data-ttu-id="ecc00-207">Por ejemplo, Detección de amenazas detecta determinadas actividades anómalas en la base de datos que sugieren posibles intentos de inyección de código SQL.</span><span class="sxs-lookup"><span data-stu-id="ecc00-207">For example, Threat Detection detects certain anomalous database activities indicating potential SQL injection attempts.</span></span> <span data-ttu-id="ecc00-208">Inyección de código SQL es uno de hello Web aplicación problemas de seguridad comunes en hello Internet, aplicaciones usadas tooattack controladas por datos.</span><span class="sxs-lookup"><span data-stu-id="ecc00-208">SQL injection is one of hello common Web application security issues on hello Internet, used tooattack data-driven applications.</span></span> <span data-ttu-id="ecc00-209">Los atacantes aprovechar aplicación vulnerabilidades tooinject instrucciones SQL malintencionadas en campos de entrada de la aplicación, para la infracción o modificar datos en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ecc00-209">Attackers take advantage of application vulnerabilities tooinject malicious SQL statements into application entry fields, for breaching or modifying data in hello database.</span></span>

1. <span data-ttu-id="ecc00-210">Navegue toohello hoja de configuración de base de datos SQL que desee toomonitor hello.</span><span class="sxs-lookup"><span data-stu-id="ecc00-210">Navigate toohello configuration blade of hello SQL database you want toomonitor.</span></span> <span data-ttu-id="ecc00-211">En la hoja de configuración de hello, seleccione **auditoría y la detección de amenazas**.</span><span class="sxs-lookup"><span data-stu-id="ecc00-211">In hello Settings blade, select **Auditing & Threat Detection**.</span></span>

    ![Panel de navegación](./media/sql-database-security-tutorial/auditing-get-started-settings.png)
2. <span data-ttu-id="ecc00-213">Hola **auditoría y la detección de amenazas** hoja de configuración a su vez **ON** auditoría, que mostrarán opciones de detección de amenazas de Hola.</span><span class="sxs-lookup"><span data-stu-id="ecc00-213">In hello **Auditing & Threat Detection** configuration blade turn **ON** auditing, which will display hello threat detection settings.</span></span>

3. <span data-ttu-id="ecc00-214">**Active** la detección de amenazas.</span><span class="sxs-lookup"><span data-stu-id="ecc00-214">Turn **ON** threat detection.</span></span>

4. <span data-ttu-id="ecc00-215">Configurar la lista de Hola de mensajes de correo electrónico que recibirán las alertas de seguridad tras la detección de actividades anómalas de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="ecc00-215">Configure hello list of emails that will receive security alerts upon detection of anomalous database activities.</span></span>

5. <span data-ttu-id="ecc00-216">Haga clic en **guardar** en hello **detección de auditoría y amenaza** hoja toosave Hola nuevo o actualizado directiva de detección de amenaza y auditoría.</span><span class="sxs-lookup"><span data-stu-id="ecc00-216">Click **Save** in hello **Auditing & Threat detection** blade toosave hello new or updated auditing and threat detection policy.</span></span>

    ![Panel de navegación](./media/sql-database-security-tutorial/td-turn-on-threat-detection.png)

    <span data-ttu-id="ecc00-218">Si se detectan actividades anómalas en la base de datos, recibirá una notificación por correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="ecc00-218">If anomalous database activities are detected, you will receive an email notification upon detection of anomalous database activities.</span></span> <span data-ttu-id="ecc00-219">correo electrónico de Hello proporcionará información sobre eventos de seguridad sospechosos de hello incluidos naturaleza Hola de actividades anómalas hello, el nombre de base de datos, hora del evento de hello y nombre de servidor.</span><span class="sxs-lookup"><span data-stu-id="ecc00-219">hello email will provide information on hello suspicious security event including hello nature of hello anomalous activities, database name, server name and hello event time.</span></span> <span data-ttu-id="ecc00-220">Además, se proporcionará información sobre las posibles causas y recomienda acciones tooinvestigate y mitigar la base de datos de toohello de amenaza potencial de Hola.</span><span class="sxs-lookup"><span data-stu-id="ecc00-220">In addition, it will provide information on possible causes and recommended actions tooinvestigate and mitigate hello potential threat toohello database.</span></span> <span data-ttu-id="ecc00-221">recorrido Hola de pasos siguiente le guían a través de qué toodo debería recibir un mensaje de correo electrónico:</span><span class="sxs-lookup"><span data-stu-id="ecc00-221">hello next steps walk you through what toodo should you receive such an email:</span></span>

    ![Correo electrónico de detección de amenazas](./media/sql-database-threat-detection-get-started/4_td_email.png)

6. <span data-ttu-id="ecc00-223">En correo electrónico de hello, haga clic en hello **el registro de auditoría de SQL de Azure** vínculo, que se inicie Hola portal de Azure y mostrar registros de auditoría relevantes de hello aproximadamente hora de Hola de eventos sospechosos Hola.</span><span class="sxs-lookup"><span data-stu-id="ecc00-223">In hello email, click on hello **Azure SQL Auditing Log** link, which will launch hello Azure portal and show hello relevant auditing records around hello time of hello suspicious event.</span></span>

    ![Registros de auditoría](./media/sql-database-threat-detection-get-started/5_td_audit_records.png)

7. <span data-ttu-id="ecc00-225">Haga clic en tooview de registros de auditoría de hello más detalles sobre las actividades de base de datos sospechosa hello como instrucción SQL, IP de cliente y el motivo del error.</span><span class="sxs-lookup"><span data-stu-id="ecc00-225">Click on hello audit records tooview more details on hello suspicious database activities such as SQL statement, failure reason and client IP.</span></span>

    ![Detalles del registro](./media/sql-database-security-tutorial/6_td_audit_record_details.png)

8. <span data-ttu-id="ecc00-227">En la hoja de registros de auditoría de hello, haga clic en **abierto en Excel** tooopen configurada previamente excel tooimport de plantilla y ejecución análisis más profundos de registro de auditoría de hello aproximadamente hora de Hola de eventos sospechosos Hola.</span><span class="sxs-lookup"><span data-stu-id="ecc00-227">In hello Auditing Records blade, click  **Open in Excel** tooopen a pre-configured excel template tooimport and run deeper analysis of hello audit log around hello time of hello suspicious event.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ecc00-228">En Excel 2010 o posterior, Power Query y hello **combinación rápida** configuración es necesaria.</span><span class="sxs-lookup"><span data-stu-id="ecc00-228">In Excel 2010 or later, Power Query and hello **Fast Combine** setting is required.</span></span>

    ![Abrir registros en Excel](./media/sql-database-threat-detection-get-started/7_td_audit_records_open_excel.png)

9. <span data-ttu-id="ecc00-230">Hola tooconfigure **combinación rápida** configuración - Hola **POWER QUERY** ficha de cinta de opciones, seleccione **opciones** cuadro de diálogo de opciones de toodisplay Hola.</span><span class="sxs-lookup"><span data-stu-id="ecc00-230">tooconfigure hello **Fast Combine** setting - In hello **POWER QUERY** ribbon tab, select **Options** toodisplay hello Options dialog.</span></span> <span data-ttu-id="ecc00-231">Seleccione la sección de privacidad de Hola y elige Hola segunda opción - 'Ignorar los niveles de privacidad de Hola y mejorar el rendimiento potencialmente':</span><span class="sxs-lookup"><span data-stu-id="ecc00-231">Select hello Privacy section and choose hello second option - 'Ignore hello Privacy Levels and potentially improve performance':</span></span>

    ![Combinación rápida de Excel](./media/sql-database-threat-detection-get-started/8_td_excel_fast_combine.png)

10. <span data-ttu-id="ecc00-233">registros de auditoría SQL tooload, asegúrese de que parámetros hello en la pestaña de configuración de hello están establecidos correctamente y, a continuación, seleccione la cinta de opciones de "Datos" hello y haga clic en botón 'Actualizar todo' hello.</span><span class="sxs-lookup"><span data-stu-id="ecc00-233">tooload SQL audit logs, ensure that hello parameters in hello settings tab are set correctly and then select hello 'Data' ribbon and click hello 'Refresh All' button.</span></span>

    ![Parámetros de Excel](./media/sql-database-threat-detection-get-started/9_td_excel_parameters.png)

11. <span data-ttu-id="ecc00-235">los resultados de Hello aparecen en hello **los registros de auditoría de SQL** hoja que le permite realizar análisis más profundos toorun actividades anómalas de Hola que se detectaron y mitigar el impacto de Hola de eventos de seguridad de hello en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ecc00-235">hello results appear in hello **SQL Audit Logs** sheet which enables you toorun deeper analysis of hello anomalous activities that were detected, and mitigate hello impact of hello security event in your application.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ecc00-236">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ecc00-236">Next steps</span></span>
<span data-ttu-id="ecc00-237">Puede mejorar la protección de hello de la base de datos frente a accesos no autorizados con unos pocos pasos sencillos o usuarios malintencionados.</span><span class="sxs-lookup"><span data-stu-id="ecc00-237">You can improve hello protection of your database against malicious users or unauthorized access with just a few simple steps.</span></span> <span data-ttu-id="ecc00-238">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="ecc00-238">In this tutorial you learn to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="ecc00-239">Configurar reglas de firewall para un servidor o una base de datos</span><span class="sxs-lookup"><span data-stu-id="ecc00-239">Set up firewall rules for your sever and or database</span></span>
> * <span data-ttu-id="ecc00-240">Conéctese utilizando una cadena de conexión segura de base de datos de tooyour</span><span class="sxs-lookup"><span data-stu-id="ecc00-240">Connect tooyour database using a secure connection string</span></span>
> * <span data-ttu-id="ecc00-241">Administrar el acceso de los usuarios</span><span class="sxs-lookup"><span data-stu-id="ecc00-241">Manage user access</span></span>
> * <span data-ttu-id="ecc00-242">Protección de los datos con cifrado</span><span class="sxs-lookup"><span data-stu-id="ecc00-242">Protect your data with encryption</span></span>
> * <span data-ttu-id="ecc00-243">Habilitación de la auditoría de SQL Database</span><span class="sxs-lookup"><span data-stu-id="ecc00-243">Enable SQL Database auditing</span></span>
> * <span data-ttu-id="ecc00-244">Habilitación de la detección de amenazas de SQL Database</span><span class="sxs-lookup"><span data-stu-id="ecc00-244">Enable SQL Database threat detection</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="ecc00-245">Mejora del rendimiento de SQL Database</span><span class="sxs-lookup"><span data-stu-id="ecc00-245">Improve SQL Database performance</span></span>](sql-database-performance-tutorial.md)

