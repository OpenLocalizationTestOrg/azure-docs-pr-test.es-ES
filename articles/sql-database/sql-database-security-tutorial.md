---
title: "Protección de la base de datos de Azure SQL | Microsoft Docs"
description: "Conozca las técnicas y características para proteger su base de datos de Azure SQL."
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
ms.openlocfilehash: 4bc09ad13ed0c9dc9257e9c75ec6f9ff3d689a0b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="secure-your-azure-sql-database"></a><span data-ttu-id="0b415-103">Protección de Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="0b415-103">Secure your Azure SQL Database</span></span>

<span data-ttu-id="0b415-104">SQL Database protege los datos mediante la limitación del acceso a la base de datos a través de reglas de firewall, de mecanismos de autenticación que requieren que los usuarios prueben su identidad y de la autorización a través de pertenencias y permisos basados en roles, así como la seguridad de nivel de fila y el enmascaramiento dinámico de datos.</span><span class="sxs-lookup"><span data-stu-id="0b415-104">SQL Database secures your data by limiting access to your database using firewall rules, authentication mechanisms requiring users to prove their identity, and authorization to data through role-based memberships and permissions, as well as through row-level security and dynamic data masking.</span></span>

<span data-ttu-id="0b415-105">Con unos pocos pasos sencillos puede mejorar la protección de su base de datos contra usuarios malintencionados o acceso no autorizado.</span><span class="sxs-lookup"><span data-stu-id="0b415-105">You can improve the protection of your database against malicious users or unauthorized access with just a few simple steps.</span></span> <span data-ttu-id="0b415-106">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="0b415-106">In this tutorial you learn to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="0b415-107">Configurar reglas de firewall de nivel de servidor para el servidor en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0b415-107">Set up server-level firewall rules for your server in the Azure portal</span></span>
> * <span data-ttu-id="0b415-108">Configurar reglas de firewall de nivel de base de datos para la base de datos con SSMS</span><span class="sxs-lookup"><span data-stu-id="0b415-108">Set up database-level firewall rules for your database using SSMS</span></span>
> * <span data-ttu-id="0b415-109">Conexión a una base de datos mediante una cadena de conexión segura</span><span class="sxs-lookup"><span data-stu-id="0b415-109">Connect to your database using a secure connection string</span></span>
> * <span data-ttu-id="0b415-110">Administrar el acceso de los usuarios</span><span class="sxs-lookup"><span data-stu-id="0b415-110">Manage user access</span></span>
> * <span data-ttu-id="0b415-111">Protección de los datos con cifrado</span><span class="sxs-lookup"><span data-stu-id="0b415-111">Protect your data with encryption</span></span>
> * <span data-ttu-id="0b415-112">Habilitación de la auditoría de SQL Database</span><span class="sxs-lookup"><span data-stu-id="0b415-112">Enable SQL Database auditing</span></span>
> * <span data-ttu-id="0b415-113">Habilitación de la detección de amenazas de SQL Database</span><span class="sxs-lookup"><span data-stu-id="0b415-113">Enable SQL Database threat detection</span></span>

<span data-ttu-id="0b415-114">Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="0b415-114">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0b415-115">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0b415-115">Prerequisites</span></span>

<span data-ttu-id="0b415-116">Para completar este tutorial, asegúrese de lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="0b415-116">To complete this tutorial, make sure you have the following:</span></span>

- <span data-ttu-id="0b415-117">Se ha instalado la versión más reciente de [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="0b415-117">Installed the newest version of [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span></span> 
- <span data-ttu-id="0b415-118">Se ha instalado Microsoft Excel</span><span class="sxs-lookup"><span data-stu-id="0b415-118">Installed Microsoft Excel</span></span>
- <span data-ttu-id="0b415-119">Se ha creado una base de datos y un servidor de SQL Azure: vea [Creación de una base de datos de Azure SQL Database en Azure Portal](sql-database-get-started-portal.md), [Creación de una sola base de datos de Azure SQL Database con la CLI de Azure](sql-database-get-started-cli.md) y [Creación de una sola base de datos de Azure SQL Database con PowerShell](sql-database-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="0b415-119">Created an Azure SQL server and database - See [Create an Azure SQL database in the Azure portal](sql-database-get-started-portal.md), [Create a single Azure SQL database using the Azure CLI](sql-database-get-started-cli.md), and [Create a single Azure SQL database using PowerShell](sql-database-get-started-powershell.md).</span></span> 

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="0b415-120">Inicio de sesión en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0b415-120">Log in to the Azure portal</span></span>

<span data-ttu-id="0b415-121">Inicie sesión en [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0b415-121">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-server-level-firewall-rule-in-the-azure-portal"></a><span data-ttu-id="0b415-122">Creación de una regla de firewall de nivel a servidor en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0b415-122">Create a server-level firewall rule in the Azure portal</span></span>

<span data-ttu-id="0b415-123">En Azure, las bases de datos SQL están protegidas mediante un firewall.</span><span class="sxs-lookup"><span data-stu-id="0b415-123">SQL databases are protected by a firewall in Azure.</span></span> <span data-ttu-id="0b415-124">De forma predeterminada, todas las conexiones al servidor y a las bases de datos que contiene se rechazan, excepto las conexiones desde otros servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="0b415-124">By default, all connections to the server and the databases inside the server are rejected except for connections from other Azure services.</span></span> <span data-ttu-id="0b415-125">Para más información, consulte [Reglas de firewall de nivel de base de datos y de nivel de servidor de Azure SQL Database](sql-database-firewall-configure.md).</span><span class="sxs-lookup"><span data-stu-id="0b415-125">For more information, see [Azure SQL Database server-level and database-level firewall rules](sql-database-firewall-configure.md).</span></span>

<span data-ttu-id="0b415-126">La opción más segura es seleccionar Desactivado en "Permitir el acceso a servicios de Azure".</span><span class="sxs-lookup"><span data-stu-id="0b415-126">The most secure configuration is to set 'Allow access to Azure services' to OFF.</span></span> <span data-ttu-id="0b415-127">Si necesita conectarse a la base de datos desde una máquina virtual o un servicio en la nube de Azure, debe crear una [IP reservada](../virtual-network/virtual-networks-reserved-public-ip.md) y permitir que solo la IP reservada acceda a través del firewall.</span><span class="sxs-lookup"><span data-stu-id="0b415-127">If you need to connect to the database from an Azure VM or cloud service, you should create a [Reserved IP](../virtual-network/virtual-networks-reserved-public-ip.md) and allow only the reserved IP address access through the firewall.</span></span> 

<span data-ttu-id="0b415-128">Siga estos pasos para crear una [regla de firewall de nivel de servidor de SQL Database](sql-database-firewall-configure.md) para el servidor, a fin de permitir conexiones desde una dirección IP específica.</span><span class="sxs-lookup"><span data-stu-id="0b415-128">Follow these steps to create a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your server to allow connections from a specific IP address.</span></span> 

> [!NOTE]
> <span data-ttu-id="0b415-129">Si ha creado una base de datos de ejemplo en Azure mediante una de las plantillas de inicio rápido o de los tutoriales anteriores, y está siguiendo este en un equipo con la misma dirección IP que tenía cuando seguía esos tutoriales, puede omitir este paso ya que se habrá creado una regla de firewall de nivel de servidor.</span><span class="sxs-lookup"><span data-stu-id="0b415-129">If you have created a sample database in Azure using one of the previous tutorials or quickstarts and are performing this tutorial on a computer with the same IP address that it had when you walked through those tutorials, you can skip this step as you will have already created a server-level firewall rule.</span></span>
>

1. <span data-ttu-id="0b415-130">Haga clic en **Bases de datos SQL** en el menú izquierdo y haga clic en la base de datos para la que desea configurar la regla de firewall en la página **Bases de datos SQL**.</span><span class="sxs-lookup"><span data-stu-id="0b415-130">Click **SQL databases** from the left-hand menu and click the database you would like to configure the firewall rule for on the **SQL databases** page.</span></span> <span data-ttu-id="0b415-131">Se abre la página de información general de la base de datos, que muestra el nombre completo del servidor (por ejemplo, **mynewserver-20170313.database.windows.net**) y proporciona opciones para otras configuraciones.</span><span class="sxs-lookup"><span data-stu-id="0b415-131">The overview page for your database opens, showing you the fully qualified server name (such as **mynewserver-20170313.database.windows.net**) and provides options for further configuration.</span></span>

      ![regla de firewall del servidor](./media/sql-database-security-tutorial/server-firewall-rule.png) 

2. <span data-ttu-id="0b415-133">Haga clic en **Establecer el firewall del servidor** en la barra de herramientas, como se muestra en la imagen anterior.</span><span class="sxs-lookup"><span data-stu-id="0b415-133">Click **Set server firewall** on the toolbar as shown in the previous image.</span></span> <span data-ttu-id="0b415-134">Se abrirá la página **Configuración del firewall** del servidor de SQL Database.</span><span class="sxs-lookup"><span data-stu-id="0b415-134">The **Firewall settings** page for the SQL Database server opens.</span></span> 

3. <span data-ttu-id="0b415-135">Haga clic en **Agregar IP de cliente** en la barra de herramientas para agregar la dirección IP pública del equipo conectado al portal o escriba manualmente la regla de firewall y luego haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0b415-135">Click **Add client IP** on the toolbar to add the public IP address of the computer connected to the portal with or enter the firewall rule manually and then click **Save**.</span></span>

      ![establecer regla de firewall del servidor](./media/sql-database-security-tutorial/server-firewall-rule-set.png) 

4. <span data-ttu-id="0b415-137">Haga clic en **Aceptar** y, después, en la **X** para cerrar la página **Configuración de firewall**.</span><span class="sxs-lookup"><span data-stu-id="0b415-137">Click **OK** and then click the **X** to close the **Firewall settings** page.</span></span>

<span data-ttu-id="0b415-138">Ahora puede conectarse a cualquier base de datos del servidor con la dirección IP o el intervalo de direcciones IP especificados.</span><span class="sxs-lookup"><span data-stu-id="0b415-138">You can now connect to any database in the server with the specified IP address or IP address range.</span></span>

> [!NOTE]
> <span data-ttu-id="0b415-139">SQL Database se comunica a través del puerto 1433.</span><span class="sxs-lookup"><span data-stu-id="0b415-139">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="0b415-140">Si intenta conectarse desde dentro de una red corporativa, es posible que el firewall de la red no permita el tráfico de salida a través del puerto 1433.</span><span class="sxs-lookup"><span data-stu-id="0b415-140">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="0b415-141">Si es así, no podrá conectarse al servidor de Azure SQL Database, a menos que el departamento de TI abra el puerto 1433.</span><span class="sxs-lookup"><span data-stu-id="0b415-141">If so, you will not be able to connect to your Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-level-firewall-rule-using-ssms"></a><span data-ttu-id="0b415-142">Creación de una regla de firewall de nivel de base de datos con SSMS</span><span class="sxs-lookup"><span data-stu-id="0b415-142">Create a database-level firewall rule using SSMS</span></span>

<span data-ttu-id="0b415-143">Las reglas de firewall de nivel de base de datos le permiten crear una configuración de firewall diferente para bases de datos distintas dentro del mismo servidor lógico y crear reglas de firewall que sean portátiles, lo que significa que siguen la base de datos durante una [conmutación por error](sql-database-geo-replication-overview.md) en lugar de almacenarse en el servidor SQL.</span><span class="sxs-lookup"><span data-stu-id="0b415-143">Database-level firewall rules enable you to create different firewall settings for different databases within the same logical server and to create firewall rules that are portable - meaning that they follow the database during a [failover](sql-database-geo-replication-overview.md) rather than being stored on the SQL server.</span></span> <span data-ttu-id="0b415-144">Las reglas de firewall de nivel de base de datos solo pueden configurarse mediante instrucciones Transact-SQL y solo después de haber configurado la primera regla de firewall de nivel de servidor.</span><span class="sxs-lookup"><span data-stu-id="0b415-144">Database-level firewall rules can only be configured by using Transact-SQL statements and only after you have configured the first server-level firewall rule.</span></span> <span data-ttu-id="0b415-145">Para más información, consulte [Reglas de firewall de nivel de base de datos y de nivel de servidor de Azure SQL Database](sql-database-firewall-configure.md).</span><span class="sxs-lookup"><span data-stu-id="0b415-145">For more information, see [Azure SQL Database server-level and database-level firewall rules](sql-database-firewall-configure.md).</span></span>

<span data-ttu-id="0b415-146">Siga estos pasos para crear una regla de firewall específica de base de datos.</span><span class="sxs-lookup"><span data-stu-id="0b415-146">Follows these steps to create a database-specific firewall rule.</span></span>

1. <span data-ttu-id="0b415-147">Conéctese a la base de datos, para lo que puede usar, por ejemplo, [SQL Server Management Studio](./sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="0b415-147">Connect to your database, for example using [SQL Server Management Studio](./sql-database-connect-query-ssms.md).</span></span>

2. <span data-ttu-id="0b415-148">En el Explorador de objetos, haga clic con el botón derecho en la base de datos para la que quiere agregar una regla de firewall y haga clic en **Nueva consulta**.</span><span class="sxs-lookup"><span data-stu-id="0b415-148">In Object Explorer, right-click on the database you want to add a firewall rule for and click **New Query**.</span></span> <span data-ttu-id="0b415-149">Se abre una ventana de consulta en blanco que está conectada a la base de datos.</span><span class="sxs-lookup"><span data-stu-id="0b415-149">A blank query window opens that is connected to your database.</span></span>

3. <span data-ttu-id="0b415-150">En la ventana de consulta, modifique la dirección IP con su dirección IP pública y, a continuación, ejecute la siguiente consulta:</span><span class="sxs-lookup"><span data-stu-id="0b415-150">In the query window, modify the IP address to your public IP address and then execute the following query:</span></span>

    ```sql
    EXECUTE sp_set_database_firewall_rule N'Example DB Rule','0.0.0.4','0.0.0.4';
    ```

4. <span data-ttu-id="0b415-151">En la barra de herramientas, haga clic en **Ejecutar** para crear la regla de firewall.</span><span class="sxs-lookup"><span data-stu-id="0b415-151">On the toolbar, click **Execute** to create the firewall rule.</span></span>

## <a name="view-how-to-connect-an-application-to-your-database-using-a-secure-connection-string"></a><span data-ttu-id="0b415-152">Vea cómo conectar una aplicación a una base de datos con una cadena de conexión segura</span><span class="sxs-lookup"><span data-stu-id="0b415-152">View how to connect an application to your database using a secure connection string</span></span>

<span data-ttu-id="0b415-153">Para garantizar una conexión cifrada y segura entre una aplicación cliente y SQL Database, la cadena de conexión debe estar configurada para:</span><span class="sxs-lookup"><span data-stu-id="0b415-153">To ensure a secure, encrypted connection between a client application and SQL Database, the connection string has to be configured to:</span></span>

- <span data-ttu-id="0b415-154">Solicitar una conexión cifrada y</span><span class="sxs-lookup"><span data-stu-id="0b415-154">Request an encrypted connection, and</span></span>
- <span data-ttu-id="0b415-155">No confiar en el certificado de servidor.</span><span class="sxs-lookup"><span data-stu-id="0b415-155">To not trust the server certificate.</span></span> 

<span data-ttu-id="0b415-156">De esta forma se establece una conexión mediante Seguridad de la capa de transporte (TLS) y se reduce el riesgo de ataques de tipo "Man in the middle".</span><span class="sxs-lookup"><span data-stu-id="0b415-156">This establishes a connection using Transport Layer Security (TLS) and reduces the risk of man-in-the-middle attacks.</span></span> <span data-ttu-id="0b415-157">Para obtener cadenas de conexión configuradas correctamente para SQL Database para los controladores de cliente admitidos, vaya a Azure Portal, como se muestra en la captura de pantalla para ADO.net.</span><span class="sxs-lookup"><span data-stu-id="0b415-157">You can obtain correctly configured connection strings for your SQL Database for supported client drivers from the Azure portal as shown for ADO.net in this screenshot.</span></span>

1. <span data-ttu-id="0b415-158">Seleccione **Bases de datos SQL** en el menú de la izquierda y haga clic en la base de datos en la página **Bases de datos SQL**.</span><span class="sxs-lookup"><span data-stu-id="0b415-158">Select **SQL databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span>

2. <span data-ttu-id="0b415-159">En la página **Overview** (Información general), haga clic en **Mostrar las cadenas de conexión de la base de datos**.</span><span class="sxs-lookup"><span data-stu-id="0b415-159">On the **Overview** page for your database, click **Show database connection strings**.</span></span>

3. <span data-ttu-id="0b415-160">Revise la cadena de conexión completa de **ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="0b415-160">Review the complete **ADO.NET** connection string.</span></span>

    ![Cadena de conexión ADO.NET](./media/sql-database-security-tutorial/adonet-connection-string.png)

## <a name="creating-database-users"></a><span data-ttu-id="0b415-162">Creación de usuarios de base de datos</span><span class="sxs-lookup"><span data-stu-id="0b415-162">Creating database users</span></span>

<span data-ttu-id="0b415-163">Antes de crear los usuarios, primero debe elegir uno de dos tipos de autenticación admitidos por Azure SQL Database:</span><span class="sxs-lookup"><span data-stu-id="0b415-163">Before creating any users, you must first choose from one of two authentication types supported by Azure SQL Database:</span></span> 

<span data-ttu-id="0b415-164">**Autenticación de SQL**, que usa el nombre de usuario y la contraseña para inicios de sesión y usuarios que son válidos únicamente en el contexto de una base de datos específica dentro de un servidor lógico.</span><span class="sxs-lookup"><span data-stu-id="0b415-164">**SQL Authentication**, which uses username and password for logins and users that are valid only in the context of a specific database within a logical server.</span></span> 

<span data-ttu-id="0b415-165">**Autenticación de Azure Active Directory**, que usa identidades administradas por Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0b415-165">**Azure Active Directory Authentication**, which uses identities managed by Azure Active Directory.</span></span> 

<span data-ttu-id="0b415-166">Si desea usar [Azure Active Directory](./sql-database-aad-authentication.md) para autenticarse en SQL Database, debe existir una instancia de Azure Active Directory rellenada antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="0b415-166">If you want to use [Azure Active Directory](./sql-database-aad-authentication.md) to authenticate against SQL Database, a populated Azure Active Directory must exist before you can proceed.</span></span>

<span data-ttu-id="0b415-167">Siga estos pasos para crear un usuario mediante la autenticación de SQL:</span><span class="sxs-lookup"><span data-stu-id="0b415-167">Follow these steps to create a user using SQL Authentication:</span></span>

1. <span data-ttu-id="0b415-168">Conéctese a la base de datos, para lo que puede usar, por ejemplo, [SQL Server Management Studio](./sql-database-connect-query-ssms.md) con sus credenciales de administrador de servidor.</span><span class="sxs-lookup"><span data-stu-id="0b415-168">Connect to your database, for example using [SQL Server Management Studio](./sql-database-connect-query-ssms.md) using your server admin credentials.</span></span>

2. <span data-ttu-id="0b415-169">En el Explorador de objetos, haga clic con el botón derecho en la base de datos a la que quiere agregar un nuevo usuario y haga clic en **Nueva consulta**.</span><span class="sxs-lookup"><span data-stu-id="0b415-169">In Object Explorer, right-click on the database you want to add a new user on and click **New Query**.</span></span> <span data-ttu-id="0b415-170">Se abre una ventana de consulta en blanco que está conectada a la base de datos seleccionada.</span><span class="sxs-lookup"><span data-stu-id="0b415-170">A blank query window opens that is connected to the selected database.</span></span>

3. <span data-ttu-id="0b415-171">En la ventana Consulta, escriba la consulta siguiente:</span><span class="sxs-lookup"><span data-stu-id="0b415-171">In the query window, enter the following query:</span></span>

    ```sql
    CREATE USER ApplicationUser WITH PASSWORD = 'YourStrongPassword1';
    ```

4. <span data-ttu-id="0b415-172">En la barra de herramientas, haga clic en **Ejecutar** para crear el usuario.</span><span class="sxs-lookup"><span data-stu-id="0b415-172">On the toolbar, click **Execute** to create the user.</span></span>

5. <span data-ttu-id="0b415-173">De forma predeterminada, el usuario puede conectarse a la base de datos, pero no tiene permisos para leer o escribir datos.</span><span class="sxs-lookup"><span data-stu-id="0b415-173">By default, the user can connect to the database, but has no permissions to read or write data.</span></span> <span data-ttu-id="0b415-174">Para conceder estos permisos al usuario recién creado, ejecute los dos comandos siguientes en una nueva ventana de consulta</span><span class="sxs-lookup"><span data-stu-id="0b415-174">To grant these permissions to the newly created user, execute the following two commands in a new query window</span></span>

    ```sql
    ALTER ROLE db_datareader ADD MEMBER ApplicationUser;
    ALTER ROLE db_datawriter ADD MEMBER ApplicationUser;
    ```

<span data-ttu-id="0b415-175">Es aconsejable crear estas cuentas sin privilegios de administrador en el nivel de base de datos para conectarse a la base de datos a menos que necesite ejecutar tareas de administrador, como crear nuevos usuarios.</span><span class="sxs-lookup"><span data-stu-id="0b415-175">It is best practice to create these non-administrator accounts at the database level to connect to your database unless you need to execute administrator tasks like creating new users.</span></span> <span data-ttu-id="0b415-176">Revise el [tutorial de Azure Active Directory](./sql-database-aad-authentication-configure.md) sobre cómo autenticarse con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0b415-176">Please review the [Azure Active Directory tutorial](./sql-database-aad-authentication-configure.md) on how to authenticate using Azure Active Directory.</span></span>


## <a name="protect-your-data-with-encryption"></a><span data-ttu-id="0b415-177">Protección de los datos con cifrado</span><span class="sxs-lookup"><span data-stu-id="0b415-177">Protect your data with encryption</span></span>

<span data-ttu-id="0b415-178">El cifrado de datos transparente (TDE) de Azure SQL Database cifra automáticamente los datos en reposo, sin exigir ningún cambio en la aplicación que accede a la base de datos cifrada.</span><span class="sxs-lookup"><span data-stu-id="0b415-178">Azure SQL Database transparent data encryption (TDE) automatically encrypts your data at rest, without requiring any changes to the application accessing the encrypted database.</span></span> <span data-ttu-id="0b415-179">Para las bases de datos recién creadas, el TDE está activado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="0b415-179">For newly created databases, TDE is on by default.</span></span> <span data-ttu-id="0b415-180">Para habilitar el TDE para la base de datos o para comprobar que está activado, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="0b415-180">To enable TDE for your database or to verify that TDE is on, follow these steps:</span></span>

1. <span data-ttu-id="0b415-181">Seleccione **Bases de datos SQL** en el menú de la izquierda y haga clic en la base de datos en la página **Bases de datos SQL**.</span><span class="sxs-lookup"><span data-stu-id="0b415-181">Select **SQL databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 

2. <span data-ttu-id="0b415-182">Haga clic en **Cifrado de datos transparente** para abrir la página de configuración de TDE.</span><span class="sxs-lookup"><span data-stu-id="0b415-182">Click on **Transparent data encryption** to open the configuration page for TDE.</span></span>

    ![Cifrado de datos transparente](./media/sql-database-security-tutorial/transparent-data-encryption-enabled.png)

3. <span data-ttu-id="0b415-184">Si es necesario, establezca **Cifrado de datos** en Activado y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0b415-184">If necessary, set **Data encryption** to ON and click **Save**.</span></span>

<span data-ttu-id="0b415-185">Se inicia el proceso de cifrado en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="0b415-185">The encryption process starts in the background.</span></span> <span data-ttu-id="0b415-186">Para supervisar el progreso, conéctese a SQL Database mediante [SQL Server Management Studio](./sql-database-connect-query-ssms.md) consultando la columna encryption_state de la vista `sys.dm_database_encryption_keys`.</span><span class="sxs-lookup"><span data-stu-id="0b415-186">You can monitor the progress by connecting to SQL Database using [SQL Server Management Studio](./sql-database-connect-query-ssms.md) by querying the encryption_state column of the `sys.dm_database_encryption_keys` view.</span></span>

## <a name="enable-sql-database-auditing-if-necessary"></a><span data-ttu-id="0b415-187">Habilitación de la auditoría de SQL Database, si es necesario</span><span class="sxs-lookup"><span data-stu-id="0b415-187">Enable SQL Database auditing, if necessary</span></span>

<span data-ttu-id="0b415-188">Auditoría de Azure SQL Database realiza un seguimiento de eventos de bases de datos y registra los eventos en un registro de auditoría de la cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="0b415-188">Azure SQL Database Auditing tracks database events and writes them to an audit log in your Azure Storage account.</span></span> <span data-ttu-id="0b415-189">La auditoría puede ayudarle a mantener el cumplimiento de normativas y conocer la actividad de las bases de datos, así como las discrepancias y anomalías que pueden indicar la existencia de potenciales infracciones de la seguridad.</span><span class="sxs-lookup"><span data-stu-id="0b415-189">Auditing can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate potential security violations.</span></span> <span data-ttu-id="0b415-190">Siga estos pasos para crear un directiva de auditoría predeterminada para SQL Database:</span><span class="sxs-lookup"><span data-stu-id="0b415-190">Follow these steps to create a default auditing policy for your SQL database:</span></span>

1. <span data-ttu-id="0b415-191">Seleccione **Bases de datos SQL** en el menú de la izquierda y haga clic en la base de datos en la página **Bases de datos SQL**.</span><span class="sxs-lookup"><span data-stu-id="0b415-191">Select **SQL databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 

2. <span data-ttu-id="0b415-192">En la hoja Configuración, seleccione **Auditoría y detección de amenazas**.</span><span class="sxs-lookup"><span data-stu-id="0b415-192">In the Settings blade, select **Auditing & Threat Detection**.</span></span> <span data-ttu-id="0b415-193">Observe que la auditoría de nivel de servidor está deshabilitada y hay un vínculo **Ver configuración de servidor** que le permite ver o modificar la configuración de auditoría del servidor desde este contexto.</span><span class="sxs-lookup"><span data-stu-id="0b415-193">Notice that sever-level auditing is diabled and that there is a **View server settings** link that allows you to view or modify the server auditing settings from this context.</span></span>

    ![Hoja Auditoría](./media/sql-database-security-tutorial/auditing-get-started-settings.png)

3. <span data-ttu-id="0b415-195">Si prefiere habilitar un tipo (¿o ubicación?) de auditoría distinto del especificado en el nivel de servidor, **active** la auditoría y elija el tipo de autoría **Blob** .</span><span class="sxs-lookup"><span data-stu-id="0b415-195">If you prefer to enable an Audit type (or location?) different from the one specified at the server level, turn **ON** Auditing, and choose the **Blob** Auditing Type.</span></span> <span data-ttu-id="0b415-196">Si está habilitada la auditoría de blobs del servidor, la auditoría configurada de base de datos se producirá de forma paralela a la auditoría de blobs del servidor.</span><span class="sxs-lookup"><span data-stu-id="0b415-196">If server Blob auditing is enabled, the database configured audit will exist side by side with the server Blob audit.</span></span>

    ![Activar la auditoría](./media/sql-database-security-tutorial/auditing-get-started-turn-on.png)

4. <span data-ttu-id="0b415-198">Seleccione **Detalles de almacenamiento** para abrir la hoja de almacenamiento de registros de auditoría.</span><span class="sxs-lookup"><span data-stu-id="0b415-198">Select **Storage Details** to open the Audit Logs Storage Blade.</span></span> <span data-ttu-id="0b415-199">Seleccione la cuenta de almacenamiento de Azure donde se guardarán los registros, y el período de retención, después del cual se eliminarán los registros antiguos. A continuación, haga clic en **Aceptar** en la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="0b415-199">Select the Azure storage account where logs will be saved, and the retention period, after which the old logs will be deleted, then click **OK** at the bottom.</span></span> 

   > [!TIP]
   > <span data-ttu-id="0b415-200">Use la misma cuenta de almacenamiento para todas las bases de datos auditadas con el fin de obtener el máximo partido de las plantillas de informes de auditorías.</span><span class="sxs-lookup"><span data-stu-id="0b415-200">Use the same storage account for all audited databases to get the most out of the auditing reports templates.</span></span>
   > 

5. <span data-ttu-id="0b415-201">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0b415-201">Click **Save**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0b415-202">Si quiere personalizar los eventos auditados, puede hacerlo mediante PowerShell o la API de REST (consulte la sección [Automation (PowerShell/API de REST)](sql-database-auditing.md#subheading-7) para más información.</span><span class="sxs-lookup"><span data-stu-id="0b415-202">If you want to customize the audited events, you can do this via PowerShell or REST API - see the [Automation (PowerShell / REST API)](sql-database-auditing.md#subheading-7) section for more details.</span></span>
>

## <a name="enable-sql-database-threat-detection"></a><span data-ttu-id="0b415-203">Habilitación de la detección de amenazas de SQL Database</span><span class="sxs-lookup"><span data-stu-id="0b415-203">Enable SQL Database threat detection</span></span>

<span data-ttu-id="0b415-204">Detección de amenazas ofrece un nuevo nivel de seguridad, que permite a los clientes detectar amenazas potenciales y responder a ellas a medida que se producen, gracias a las alertas de seguridad sobre actividades anómalas que se proporcionan.</span><span class="sxs-lookup"><span data-stu-id="0b415-204">Threat Detection provides a new layer of security, which enables customers to detect and respond to potential threats as they occur by providing security alerts on anomalous activities.</span></span> <span data-ttu-id="0b415-205">Los usuarios pueden explorar los eventos sospechosos mediante la auditoría de SQL Database para determinar si proceden de un intento de acceder a los datos en la base de datos, infringir su seguridad o aprovecharlos.</span><span class="sxs-lookup"><span data-stu-id="0b415-205">Users can explore the suspicious events using SQL Database Auditing to determine if they result from an attempt to access, breach or exploit data in the database.</span></span> <span data-ttu-id="0b415-206">Detección de amenazas facilita la solución de las posibles amenazas a la base de datos sin necesidad de ser un experto en seguridad ni administrar sistemas de supervisión de seguridad avanzada.</span><span class="sxs-lookup"><span data-stu-id="0b415-206">Threat Detection makes it simple to address potential threats to the database without the need to be a security expert or manage advanced security monitoring systems.</span></span>
<span data-ttu-id="0b415-207">Por ejemplo, Detección de amenazas detecta determinadas actividades anómalas en la base de datos que sugieren posibles intentos de inyección de código SQL.</span><span class="sxs-lookup"><span data-stu-id="0b415-207">For example, Threat Detection detects certain anomalous database activities indicating potential SQL injection attempts.</span></span> <span data-ttu-id="0b415-208">La inyección de código SQL es uno de los problemas de seguridad habituales entre las aplicaciones web en Internet y se usa para atacar aplicaciones controladas por datos.</span><span class="sxs-lookup"><span data-stu-id="0b415-208">SQL injection is one of the common Web application security issues on the Internet, used to attack data-driven applications.</span></span> <span data-ttu-id="0b415-209">Los atacantes aprovechan las vulnerabilidades de la aplicación para inyectar instrucciones SQL malintencionadas en los campos de entrada de la aplicación, con el fin de infringir la seguridad o modificar datos en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="0b415-209">Attackers take advantage of application vulnerabilities to inject malicious SQL statements into application entry fields, for breaching or modifying data in the database.</span></span>

1. <span data-ttu-id="0b415-210">Vaya a la hoja de configuración de Base de datos SQL que desea supervisar.</span><span class="sxs-lookup"><span data-stu-id="0b415-210">Navigate to the configuration blade of the SQL database you want to monitor.</span></span> <span data-ttu-id="0b415-211">En la hoja Configuración, seleccione **Auditoría y detección de amenazas**.</span><span class="sxs-lookup"><span data-stu-id="0b415-211">In the Settings blade, select **Auditing & Threat Detection**.</span></span>

    ![Panel de navegación](./media/sql-database-security-tutorial/auditing-get-started-settings.png)
2. <span data-ttu-id="0b415-213">En la hoja de configuración **Auditoría y detección de amenazas**, **active** la auditoría; se mostrará la configuración de detección de amenazas.</span><span class="sxs-lookup"><span data-stu-id="0b415-213">In the **Auditing & Threat Detection** configuration blade turn **ON** auditing, which will display the threat detection settings.</span></span>

3. <span data-ttu-id="0b415-214">**Active** la detección de amenazas.</span><span class="sxs-lookup"><span data-stu-id="0b415-214">Turn **ON** threat detection.</span></span>

4. <span data-ttu-id="0b415-215">Configure la lista de correos electrónicos que recibirán alertas de seguridad cuando se detecten actividades anómalas en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="0b415-215">Configure the list of emails that will receive security alerts upon detection of anomalous database activities.</span></span>

5. <span data-ttu-id="0b415-216">Haga clic en **Guardar** en la hoja **Auditoría y detección de amenazas** para guardar la directiva de auditoría y detección de amenazas nueva o actualizada.</span><span class="sxs-lookup"><span data-stu-id="0b415-216">Click **Save** in the **Auditing & Threat detection** blade to save the new or updated auditing and threat detection policy.</span></span>

    ![Panel de navegación](./media/sql-database-security-tutorial/td-turn-on-threat-detection.png)

    <span data-ttu-id="0b415-218">Si se detectan actividades anómalas en la base de datos, recibirá una notificación por correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="0b415-218">If anomalous database activities are detected, you will receive an email notification upon detection of anomalous database activities.</span></span> <span data-ttu-id="0b415-219">El correo electrónico proporciona información sobre el evento de seguridad sospechoso, en la que se incluyen la naturaleza de las actividades anómalas, el nombre de la base de datos, el nombre del servidor y la hora del evento.</span><span class="sxs-lookup"><span data-stu-id="0b415-219">The email will provide information on the suspicious security event including the nature of the anomalous activities, database name, server name and the event time.</span></span> <span data-ttu-id="0b415-220">Además, se proporcionará información sobre las posibles causas y las medidas recomendadas para investigar y mitigar la amenaza potencial para la base de datos.</span><span class="sxs-lookup"><span data-stu-id="0b415-220">In addition, it will provide information on possible causes and recommended actions to investigate and mitigate the potential threat to the database.</span></span> <span data-ttu-id="0b415-221">Los siguientes pasos le guían a través de lo que debe hacer si recibe un mensaje de correo electrónico de este tipo:</span><span class="sxs-lookup"><span data-stu-id="0b415-221">The next steps walk you through what to do should you receive such an email:</span></span>

    ![Correo electrónico de detección de amenazas](./media/sql-database-threat-detection-get-started/4_td_email.png)

6. <span data-ttu-id="0b415-223">En el correo electrónico, haga clic en el vínculo **Registro de auditoría SQL de Azure**, lo que iniciará el portal de Azure y mostrará los registros de auditoría pertinentes en torno a la hora del evento sospechoso.</span><span class="sxs-lookup"><span data-stu-id="0b415-223">In the email, click on the **Azure SQL Auditing Log** link, which will launch the Azure portal and show the relevant auditing records around the time of the suspicious event.</span></span>

    ![Registros de auditoría](./media/sql-database-threat-detection-get-started/5_td_audit_records.png)

7. <span data-ttu-id="0b415-225">Haga clic en los registros de auditoría para ver más detalles sobre las actividades sospechosas en la base de datos, como instrucción SQL, motivo del error e IP de cliente.</span><span class="sxs-lookup"><span data-stu-id="0b415-225">Click on the audit records to view more details on the suspicious database activities such as SQL statement, failure reason and client IP.</span></span>

    ![Detalles del registro](./media/sql-database-security-tutorial/6_td_audit_record_details.png)

8. <span data-ttu-id="0b415-227">En la hoja Registros de auditoría, haga clic en **Abrir en Excel** para abrir una plantilla de Excel ya configurada para importar y ejecutar un análisis más profundo del registro de auditoría en torno a la hora del evento sospechoso.</span><span class="sxs-lookup"><span data-stu-id="0b415-227">In the Auditing Records blade, click  **Open in Excel** to open a pre-configured excel template to import and run deeper analysis of the audit log around the time of the suspicious event.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0b415-228">En Excel 2010 o superior, se requieren Power Query y la opción **Combinación rápida**.</span><span class="sxs-lookup"><span data-stu-id="0b415-228">In Excel 2010 or later, Power Query and the **Fast Combine** setting is required.</span></span>

    ![Abrir registros en Excel](./media/sql-database-threat-detection-get-started/7_td_audit_records_open_excel.png)

9. <span data-ttu-id="0b415-230">Para definir la configuración **Combinación rápida**: en la pestaña **POWER QUERY** de la cinta, seleccione **Opciones** para mostrar el cuadro de diálogo Opciones.</span><span class="sxs-lookup"><span data-stu-id="0b415-230">To configure the **Fast Combine** setting - In the **POWER QUERY** ribbon tab, select **Options** to display the Options dialog.</span></span> <span data-ttu-id="0b415-231">Seleccione la sección Privacidad y elija la segunda opción, "Omitir los niveles de privacidad para mejorar el rendimiento":</span><span class="sxs-lookup"><span data-stu-id="0b415-231">Select the Privacy section and choose the second option - 'Ignore the Privacy Levels and potentially improve performance':</span></span>

    ![Combinación rápida de Excel](./media/sql-database-threat-detection-get-started/8_td_excel_fast_combine.png)

10. <span data-ttu-id="0b415-233">Para cargar registros de auditoría SQL, asegúrese de que los parámetros de la pestaña Configuración sean correctos y después seleccione "Datos" en la cinta y haga clic en el botón "Actualizar todo".</span><span class="sxs-lookup"><span data-stu-id="0b415-233">To load SQL audit logs, ensure that the parameters in the settings tab are set correctly and then select the 'Data' ribbon and click the 'Refresh All' button.</span></span>

    ![Parámetros de Excel](./media/sql-database-threat-detection-get-started/9_td_excel_parameters.png)

11. <span data-ttu-id="0b415-235">Los resultados aparecen en la hoja **Registros de auditoría SQL** , que permite ejecutar un análisis más profundo de las actividades anómalas que se detectaron y mitigar el impacto del evento de seguridad en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0b415-235">The results appear in the **SQL Audit Logs** sheet which enables you to run deeper analysis of the anomalous activities that were detected, and mitigate the impact of the security event in your application.</span></span>


## <a name="next-steps"></a><span data-ttu-id="0b415-236">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0b415-236">Next steps</span></span>
<span data-ttu-id="0b415-237">Con unos pocos pasos sencillos puede mejorar la protección de su base de datos contra usuarios malintencionados o acceso no autorizado.</span><span class="sxs-lookup"><span data-stu-id="0b415-237">You can improve the protection of your database against malicious users or unauthorized access with just a few simple steps.</span></span> <span data-ttu-id="0b415-238">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="0b415-238">In this tutorial you learn to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="0b415-239">Configurar reglas de firewall para un servidor o una base de datos</span><span class="sxs-lookup"><span data-stu-id="0b415-239">Set up firewall rules for your sever and or database</span></span>
> * <span data-ttu-id="0b415-240">Conexión a una base de datos mediante una cadena de conexión segura</span><span class="sxs-lookup"><span data-stu-id="0b415-240">Connect to your database using a secure connection string</span></span>
> * <span data-ttu-id="0b415-241">Administrar el acceso de los usuarios</span><span class="sxs-lookup"><span data-stu-id="0b415-241">Manage user access</span></span>
> * <span data-ttu-id="0b415-242">Protección de los datos con cifrado</span><span class="sxs-lookup"><span data-stu-id="0b415-242">Protect your data with encryption</span></span>
> * <span data-ttu-id="0b415-243">Habilitación de la auditoría de SQL Database</span><span class="sxs-lookup"><span data-stu-id="0b415-243">Enable SQL Database auditing</span></span>
> * <span data-ttu-id="0b415-244">Habilitación de la detección de amenazas de SQL Database</span><span class="sxs-lookup"><span data-stu-id="0b415-244">Enable SQL Database threat detection</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="0b415-245">Mejora del rendimiento de SQL Database</span><span class="sxs-lookup"><span data-stu-id="0b415-245">Improve SQL Database performance</span></span>](sql-database-performance-tutorial.md)

