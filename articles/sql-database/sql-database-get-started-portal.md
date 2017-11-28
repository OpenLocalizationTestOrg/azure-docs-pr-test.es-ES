---
title: "Azure Portal: Creación de una base de datos SQL | Microsoft Docs"
description: "Aprenda a crear un servidor lógico de SQL Database, una regla de firewall de nivel de servidor y bases de datos en Azure Portal. También aprenderá a consultar de una instancia de Azure SQL Database desde Azure Portal."
keywords: "tutorial de sql database, creación de una base de datos sql"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: aeb8c4c3-6ae2-45f7-b2c3-fa13e3752eed
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: portal
ms.devlang: na
ms.topic: hero-article
ms.date: 05/30/2017
ms.author: carlrab
ms.openlocfilehash: a863cf3ad08040906850f64db6505f30bcfa72eb
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-azure-sql-database-in-the-azure-portal"></a><span data-ttu-id="5c803-105">Creación de una instancia de Azure SQL Database en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5c803-105">Create an Azure SQL database in the Azure portal</span></span>

<span data-ttu-id="5c803-106">Este tutorial de inicio rápido le guía por el proceso de creación de una instancia de SQL Database en Azure.</span><span class="sxs-lookup"><span data-stu-id="5c803-106">This quick start tutorial walks through how to create a SQL database in Azure.</span></span> <span data-ttu-id="5c803-107">Azure SQL Database es una oferta de "base de datos como servicio" que permite ejecutar y escalar bases de datos de SQL Server de alta disponibilidad en la nube.</span><span class="sxs-lookup"><span data-stu-id="5c803-107">Azure SQL Database is a “Database-as-a-Service” offering that enables you to run and scale highly available SQL Server databases in the cloud.</span></span> <span data-ttu-id="5c803-108">En esta guía de inicio rápido se muestra cómo comenzar mediante la creación de una instancia de SQL Database a través de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="5c803-108">This quick start shows you how to get started by creating a SQL database using the Azure portal.</span></span>

<span data-ttu-id="5c803-109">Si no tiene una suscripción a Azure, cree una cuenta [gratuita](https://azure.microsoft.com/free/) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="5c803-109">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="5c803-110">Iniciar sesión en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5c803-110">Log in to the Azure portal</span></span>

<span data-ttu-id="5c803-111">Inicie sesión en [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5c803-111">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-sql-database"></a><span data-ttu-id="5c803-112">Creación de una base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="5c803-112">Create a SQL database</span></span>

<span data-ttu-id="5c803-113">Se crea una base de datos SQL de Azure con un conjunto definido de [recursos de proceso y almacenamiento](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="5c803-113">An Azure SQL database is created with a defined set of [compute and storage resources](sql-database-service-tiers.md).</span></span> <span data-ttu-id="5c803-114">La base de datos se crea dentro de un [grupo de recursos de Azure](../azure-resource-manager/resource-group-overview.md) y en un [servidor lógico de Azure SQL Database](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="5c803-114">The database is created within an [Azure resource group](../azure-resource-manager/resource-group-overview.md) and in an [Azure SQL Database logical server](sql-database-features.md).</span></span> 

<span data-ttu-id="5c803-115">Siga estos pasos para crear una base de datos SQL que contenga los datos de ejemplo de Adventure Works LT.</span><span class="sxs-lookup"><span data-stu-id="5c803-115">Follow these steps to create a SQL database containing the Adventure Works LT sample data.</span></span> 

1. <span data-ttu-id="5c803-116">Haga clic en el botón **Nuevo** de la esquina superior izquierda de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="5c803-116">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="5c803-117">En la página **Nuevo**, seleccione **Bases de datos** y, en la página **Bases de datos**, seleccione **SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="5c803-117">Select **Databases** from the **New** page, and select **SQL Database** from the **Databases** page.</span></span>

   ![create database-1](./media/sql-database-get-started-portal/create-database-1.png)

3. <span data-ttu-id="5c803-119">Rellene el formulario de SQL Database con la siguiente información, como se muestra en la imagen anterior:</span><span class="sxs-lookup"><span data-stu-id="5c803-119">Fill out the SQL Database form with the following information, as shown on the preceding image:</span></span>   

   | <span data-ttu-id="5c803-120">Configuración</span><span class="sxs-lookup"><span data-stu-id="5c803-120">Setting</span></span>       | <span data-ttu-id="5c803-121">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="5c803-121">Suggested value</span></span> | <span data-ttu-id="5c803-122">Descripción</span><span class="sxs-lookup"><span data-stu-id="5c803-122">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="5c803-123">**Nombre de la base de datos**</span><span class="sxs-lookup"><span data-stu-id="5c803-123">**Database name**</span></span> | <span data-ttu-id="5c803-124">mySampleDatabase</span><span class="sxs-lookup"><span data-stu-id="5c803-124">mySampleDatabase</span></span> | <span data-ttu-id="5c803-125">Para conocer los nombres de base de datos válidos, consulte [Database Identifiers](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers) (Identificadores de base de datos).</span><span class="sxs-lookup"><span data-stu-id="5c803-125">For valid database names, see [Database Identifiers](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers).</span></span> | 
   | <span data-ttu-id="5c803-126">**Suscripción**</span><span class="sxs-lookup"><span data-stu-id="5c803-126">**Subscription**</span></span> | <span data-ttu-id="5c803-127">Su suscripción</span><span class="sxs-lookup"><span data-stu-id="5c803-127">Your subscription</span></span>  | <span data-ttu-id="5c803-128">Para más información acerca de sus suscripciones, consulte [Suscripciones](https://account.windowsazure.com/Subscriptions).</span><span class="sxs-lookup"><span data-stu-id="5c803-128">For details about your subscriptions, see [Subscriptions](https://account.windowsazure.com/Subscriptions).</span></span> |
   | <span data-ttu-id="5c803-129">**Grupos de recursos**</span><span class="sxs-lookup"><span data-stu-id="5c803-129">**Resource group**</span></span>  | <span data-ttu-id="5c803-130">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5c803-130">myResourceGroup</span></span> | <span data-ttu-id="5c803-131">Para conocer cuáles son los nombres de grupo de recursos válidos, consulte el artículo [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Convenciones de nomenclatura).</span><span class="sxs-lookup"><span data-stu-id="5c803-131">For valid resource group names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> |
   | <span data-ttu-id="5c803-132">**Seleccionar origen**</span><span class="sxs-lookup"><span data-stu-id="5c803-132">**Source source**</span></span> | <span data-ttu-id="5c803-133">Ejemplo (AdventureWorksLT)</span><span class="sxs-lookup"><span data-stu-id="5c803-133">Sample (AdventureWorksLT)</span></span> | <span data-ttu-id="5c803-134">Carga el esquema y los datos de AdventureWorksLT en la base de datos nueva</span><span class="sxs-lookup"><span data-stu-id="5c803-134">Loads the AdventureWorksLT schema and data into your new database</span></span> |

   > [!IMPORTANT]
   > <span data-ttu-id="5c803-135">Debe seleccionar la base de datos de ejemplo de este formulario porque se utiliza en el resto de esta guía de inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="5c803-135">You must select the sample database on this form because it is used in the remainder of this quick start.</span></span>
   > 

4. <span data-ttu-id="5c803-136">En **Servidor**, haga clic en **Configurar los valores obligatorios** y rellene el formulario de SQL Server (servidor lógico) con la siguiente información, como se muestra en la imagen siguiente:</span><span class="sxs-lookup"><span data-stu-id="5c803-136">Under **Server**, click **Configure required settings** and fill out the SQL server (logical server) form with the following information, as shown on the following image:</span></span>   

   | <span data-ttu-id="5c803-137">Configuración</span><span class="sxs-lookup"><span data-stu-id="5c803-137">Setting</span></span>       | <span data-ttu-id="5c803-138">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="5c803-138">Suggested value</span></span> | <span data-ttu-id="5c803-139">Descripción</span><span class="sxs-lookup"><span data-stu-id="5c803-139">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="5c803-140">**Nombre del servidor**</span><span class="sxs-lookup"><span data-stu-id="5c803-140">**Server name**</span></span> | <span data-ttu-id="5c803-141">Cualquier nombre globalmente único</span><span class="sxs-lookup"><span data-stu-id="5c803-141">Any globally unique name</span></span> | <span data-ttu-id="5c803-142">Para conocer cuáles son los nombres de servidor válidos, consulte el artículo [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Convenciones de nomenclatura).</span><span class="sxs-lookup"><span data-stu-id="5c803-142">For valid server names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> | 
   | <span data-ttu-id="5c803-143">**Inicio de sesión del administrador del servidor**</span><span class="sxs-lookup"><span data-stu-id="5c803-143">**Server admin login**</span></span> | <span data-ttu-id="5c803-144">Cualquier nombre válido</span><span class="sxs-lookup"><span data-stu-id="5c803-144">Any valid name</span></span> | <span data-ttu-id="5c803-145">Para conocer los nombres de inicio de sesión válidos, consulte [Database Identifiers](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers) (Identificadores de base de datos).</span><span class="sxs-lookup"><span data-stu-id="5c803-145">For valid login names, see [Database Identifiers](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers).</span></span> |
   | <span data-ttu-id="5c803-146">**Password**</span><span class="sxs-lookup"><span data-stu-id="5c803-146">**Password**</span></span> | <span data-ttu-id="5c803-147">Cualquier contraseña válida</span><span class="sxs-lookup"><span data-stu-id="5c803-147">Any valid password</span></span> | <span data-ttu-id="5c803-148">La contraseña debe tener un mínimo de 8 caracteres y debe contener caracteres de tres de las siguientes categorías: caracteres en mayúsculas, caracteres en minúsculas, números y caracteres no alfanuméricos.</span><span class="sxs-lookup"><span data-stu-id="5c803-148">Your password must have at least 8 characters and must contain characters from three of the following categories: upper case characters, lower case characters, numbers, and and non-alphanumeric characters.</span></span> |
   | <span data-ttu-id="5c803-149">**Suscripción**</span><span class="sxs-lookup"><span data-stu-id="5c803-149">**Subscription**</span></span> | <span data-ttu-id="5c803-150">Su suscripción</span><span class="sxs-lookup"><span data-stu-id="5c803-150">Your subscription</span></span> | <span data-ttu-id="5c803-151">Para más información acerca de sus suscripciones, consulte [Suscripciones](https://account.windowsazure.com/Subscriptions).</span><span class="sxs-lookup"><span data-stu-id="5c803-151">For details about your subscriptions, see [Subscriptions](https://account.windowsazure.com/Subscriptions).</span></span> |
   | <span data-ttu-id="5c803-152">**Grupos de recursos**</span><span class="sxs-lookup"><span data-stu-id="5c803-152">**Resource group**</span></span> | <span data-ttu-id="5c803-153">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5c803-153">myResourceGroup</span></span> | <span data-ttu-id="5c803-154">Para conocer cuáles son los nombres de grupo de recursos válidos, consulte el artículo [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Convenciones de nomenclatura).</span><span class="sxs-lookup"><span data-stu-id="5c803-154">For valid resource group names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> |
   | <span data-ttu-id="5c803-155">**Ubicación**</span><span class="sxs-lookup"><span data-stu-id="5c803-155">**Location**</span></span> | <span data-ttu-id="5c803-156">Cualquier ubicación válida</span><span class="sxs-lookup"><span data-stu-id="5c803-156">Any valid location</span></span> | <span data-ttu-id="5c803-157">Para obtener información acerca de las regiones, consulte [Regiones de Azure](https://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="5c803-157">For information about regions, see [Azure Regions](https://azure.microsoft.com/regions/).</span></span> |

   > [!IMPORTANT]
   > <span data-ttu-id="5c803-158">Se requiere el inicio de sesión y la contraseña de administrador de servidor que especifique aquí para iniciar sesión en el servidor y a sus bases de datos más adelante en esta guía de inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="5c803-158">The server admin login and password that you specify here are required to log in to the server and its databases later in this quick start.</span></span> <span data-ttu-id="5c803-159">Recuerde o grabe esta información para su uso posterior.</span><span class="sxs-lookup"><span data-stu-id="5c803-159">Remember or record this information for later use.</span></span> 
   >  

   ![create database-server](./media/sql-database-get-started-portal/create-database-server.png)

5. <span data-ttu-id="5c803-161">Cuando haya completado el formulario, haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="5c803-161">When you have completed the form, click **Select**.</span></span>

6. <span data-ttu-id="5c803-162">Haga clic en **Plan de tarifa** para especificar el tanto el nivel de rendimiento como el nivel de servicio de la nueva base de datos.</span><span class="sxs-lookup"><span data-stu-id="5c803-162">Click **Pricing tier** to specify the service tier and performance level for your new database.</span></span> <span data-ttu-id="5c803-163">Utilice el control deslizante para seleccionar **20 DTU** y **250** GB de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="5c803-163">Use the slider to select **20 DTUs** and **250** GB of storage.</span></span> <span data-ttu-id="5c803-164">Para más información acerca de las DTU, consulte [¿Qué es una DTU?](sql-database-what-is-a-dtu.md).</span><span class="sxs-lookup"><span data-stu-id="5c803-164">For more information on DTUs, see [What is a DTU?](sql-database-what-is-a-dtu.md).</span></span>

   ![create database-s1](./media/sql-database-get-started-portal/create-database-s1.png)

7. <span data-ttu-id="5c803-166">Después de seleccionar la cantidad de DTU, haga clic en **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="5c803-166">After selected the amount of DTUs, click **Apply**.</span></span>  

8. <span data-ttu-id="5c803-167">Una vez completado el formulario de SQL Database, haga clic en **Crear** para aprovisionar la base de datos.</span><span class="sxs-lookup"><span data-stu-id="5c803-167">Now that you have completed the SQL Database form, click **Create** to provision the database.</span></span> <span data-ttu-id="5c803-168">El aprovisionamiento tarda unos minutos.</span><span class="sxs-lookup"><span data-stu-id="5c803-168">Provisioning takes a few minutes.</span></span> 

9. <span data-ttu-id="5c803-169">En la barra de herramientas, haga clic en **Notificaciones** para supervisar el proceso de implementación.</span><span class="sxs-lookup"><span data-stu-id="5c803-169">On the toolbar, click **Notifications** to monitor the deployment process.</span></span>

   ![notificación](./media/sql-database-get-started-portal/notification.png)

## <a name="create-a-server-level-firewall-rule"></a><span data-ttu-id="5c803-171">Crear una regla de firewall de nivel de servidor</span><span class="sxs-lookup"><span data-stu-id="5c803-171">Create a server-level firewall rule</span></span>

<span data-ttu-id="5c803-172">El servicio SQL Database crea un firewall en el nivel de servidor, lo que impide que herramientas y aplicaciones externas se conecten al servidor o a las bases de datos del servidor, a menos que se cree una regla de firewall para abrir el firewall para direcciones IP concretas.</span><span class="sxs-lookup"><span data-stu-id="5c803-172">The SQL Database service creates a firewall at the server-level that prevents external applications and tools from connecting to the server or any databases on the server unless a firewall rule is created to open the firewall for specific IP addresses.</span></span> <span data-ttu-id="5c803-173">Siga estos pasos para crear una [regla de firewall de nivel de servidor de SQL Database](sql-database-firewall-configure.md) para la dirección IP de su cliente y habilite la conectividad externa a través de dicho firewall solo para su dirección IP.</span><span class="sxs-lookup"><span data-stu-id="5c803-173">Follow these steps to create a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your client's IP address and enable external connectivity through the SQL Database firewall for your IP address only.</span></span> 

> [!NOTE]
> <span data-ttu-id="5c803-174">SQL Database se comunica a través del puerto 1433.</span><span class="sxs-lookup"><span data-stu-id="5c803-174">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="5c803-175">Si intenta conectarse desde dentro de una red corporativa, es posible que el firewall de la red no permita el tráfico de salida a través del puerto 1433.</span><span class="sxs-lookup"><span data-stu-id="5c803-175">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="5c803-176">En ese caso, no puede conectarse al servidor de Azure SQL Database, salvo que el departamento de TI abra el puerto 1433.</span><span class="sxs-lookup"><span data-stu-id="5c803-176">If so, you cannot connect to your Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

1. <span data-ttu-id="5c803-177">Cuando se haya finalizado la implementación, haga clic en **Bases de datos SQL** en el menú de la izquierda y, después, haga clic en **mySampleDatabase** en la página **Bases de datos SQL**.</span><span class="sxs-lookup"><span data-stu-id="5c803-177">After the deployment completes, click **SQL databases** from the left-hand menu and then click **mySampleDatabase** on the **SQL databases** page.</span></span> <span data-ttu-id="5c803-178">Se abre la página de información general de la base de datos, que muestra el nombre completo del servidor (por ejemplo, **mynewserver20170313.database.windows.net**) y proporciona opciones para configurarlo aún más.</span><span class="sxs-lookup"><span data-stu-id="5c803-178">The overview page for your database opens, showing you the fully qualified server name (such as **mynewserver20170313.database.windows.net**) and provides options for further configuration.</span></span> <span data-ttu-id="5c803-179">Copie dicho nombre, ya que lo tendrá que usar más adelante,</span><span class="sxs-lookup"><span data-stu-id="5c803-179">Copy this fully qualified server name for use later.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="5c803-180">lo necesitará para conectarse a su servidor y a sus bases de datos en los inicios rápidos posteriores.</span><span class="sxs-lookup"><span data-stu-id="5c803-180">You need this fully qualified server name to connect to your server and its databases in subsequent quick starts.</span></span>
   > 

   ![nombre del servidor](./media/sql-database-connect-query-dotnet/server-name.png) 

2. <span data-ttu-id="5c803-182">Haga clic en **Establecer el firewall del servidor** en la barra de herramientas, como se muestra en la imagen anterior.</span><span class="sxs-lookup"><span data-stu-id="5c803-182">Click **Set server firewall** on the toolbar as shown in the previous image.</span></span> <span data-ttu-id="5c803-183">Se abrirá la página **Configuración del firewall** del servidor de SQL Database.</span><span class="sxs-lookup"><span data-stu-id="5c803-183">The **Firewall settings** page for the SQL Database server opens.</span></span> 

   ![regla de firewall del servidor](./media/sql-database-get-started-portal/server-firewall-rule.png) 

3. <span data-ttu-id="5c803-185">Haga clic en **Agregar IP de cliente** en la barra de herramientas para agregar la dirección IP actual a la nueva regla de firewall.</span><span class="sxs-lookup"><span data-stu-id="5c803-185">Click **Add client IP** on the toolbar to add your current IP address to a new firewall rule.</span></span> <span data-ttu-id="5c803-186">La regla de firewall puede abrir el puerto 1433 para una única dirección IP o un intervalo de direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="5c803-186">A firewall rule can open port 1433 for a single IP address or a range of IP addresses.</span></span>

4. <span data-ttu-id="5c803-187">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="5c803-187">Click **Save**.</span></span> <span data-ttu-id="5c803-188">Se crea una regla de firewall de nivel de servidor para el puerto 1433 de la dirección IP actual en el servidor lógico.</span><span class="sxs-lookup"><span data-stu-id="5c803-188">A server-level firewall rule is created for your current IP address opening port 1433 on the logical server.</span></span>

   ![establecer regla de firewall del servidor](./media/sql-database-get-started-portal/server-firewall-rule-set.png) 

4. <span data-ttu-id="5c803-190">Haga clic en **Aceptar** y después cierre la página **Configuración de firewall**.</span><span class="sxs-lookup"><span data-stu-id="5c803-190">Click **OK** and then close the **Firewall settings** page.</span></span>

<span data-ttu-id="5c803-191">Ahora puede conectarse al servidor de SQL Database y a sus bases de datos mediante SQL Server Management Studio o cualquier otra herramienta que elija desde esta dirección IP usando la cuenta de administrador del servidor creada con anterioridad.</span><span class="sxs-lookup"><span data-stu-id="5c803-191">You can now connect to the SQL Database server and its databases using SQL Server Management Studio or another tool of your choice from this IP address using the server admin account created previously.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5c803-192">De forma predeterminada, el acceso a través del firewall de SQL Database está habilitado para todos los servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="5c803-192">By default, access through the SQL Database firewall is enabled for all Azure services.</span></span> <span data-ttu-id="5c803-193">Haga clic en **OFF** en esta página para deshabilitar todos los servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="5c803-193">Click **OFF** on this page to disable for all Azure services.</span></span>
>

## <a name="query-the-sql-database"></a><span data-ttu-id="5c803-194">Consulta a SQL Database</span><span class="sxs-lookup"><span data-stu-id="5c803-194">Query the SQL database</span></span>

<span data-ttu-id="5c803-195">Ahora que ha creado una base de datos de ejemplo en Azure, vamos a usar la herramienta de consulta integrada en Azure Portal para confirmar que puede conectarse a la base de datos y consultar los datos.</span><span class="sxs-lookup"><span data-stu-id="5c803-195">Now that you have created a sample database in Azure, let’s use the built-in query tool within the Azure portal to confirm that you can connect to the database and query the data.</span></span> 

1. <span data-ttu-id="5c803-196">En la barra de herramientas de la página SQL Database de la base de datos, haga clic en **Herramientas**.</span><span class="sxs-lookup"><span data-stu-id="5c803-196">On the SQL Database page for your database, click **Tools** on the toolbar.</span></span> <span data-ttu-id="5c803-197">Se abre la página **Herramientas**.</span><span class="sxs-lookup"><span data-stu-id="5c803-197">The **Tools** page opens.</span></span>

   ![menú herramientas](./media/sql-database-get-started-portal/tools-menu.png) 

2. <span data-ttu-id="5c803-199">Haga clic en **Editor de consultas (versión preliminar)**, en la casilla de verificación **Términos de vista previa** y en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="5c803-199">Click **Query editor (preview)**, click the **Preview terms** checkbox, and then click **OK**.</span></span> <span data-ttu-id="5c803-200">Se abre la página Editor de consultas.</span><span class="sxs-lookup"><span data-stu-id="5c803-200">The Query editor page opens.</span></span>

3. <span data-ttu-id="5c803-201">Haga clic en **Inicio de sesión** y después, cuando se le solicite, seleccione **Autenticación de servidor SQL Server** y especifique el inicio de sesión y la contraseña de administrador de servidor que creó antes.</span><span class="sxs-lookup"><span data-stu-id="5c803-201">Click **Login** and then, when prompted, select **SQL server authentication** and then provide the server admin login and password that you created earlier.</span></span>

   ![login](./media/sql-database-get-started-portal/login.png) 

4. <span data-ttu-id="5c803-203">Haga clic en **Aceptar** para iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="5c803-203">Click **OK** to log in.</span></span>

5. <span data-ttu-id="5c803-204">Una vez autenticado, escriba la siguiente consulta en el panel del editor de consultas.</span><span class="sxs-lookup"><span data-stu-id="5c803-204">After you are authenticated, type the following query in the query editor pane.</span></span>

   ```sql
   SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
   FROM SalesLT.ProductCategory pc
   JOIN SalesLT.Product p
   ON pc.productcategoryid = p.productcategoryid;
   ```

6. <span data-ttu-id="5c803-205">Haga clic en **Ejecución** y revise los resultados de la consulta en el panel **Resultados**.</span><span class="sxs-lookup"><span data-stu-id="5c803-205">Click **Run** and then review the query results in the **Results** pane.</span></span>

   ![resultados del editor de consultas](./media/sql-database-get-started-portal/query-editor-results.png)

7. <span data-ttu-id="5c803-207">Cierre la página **Editor de consultas** y la página **Herramientas**.</span><span class="sxs-lookup"><span data-stu-id="5c803-207">Close the **Query editor** page and the **Tools** page.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="5c803-208">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="5c803-208">Clean up resources</span></span>

<span data-ttu-id="5c803-209">Si no necesita estos recursos para otro inicio rápido o tutorial (consulte [Pasos siguientes](#next-steps)), puede eliminarlos de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="5c803-209">If you don't need these resources for another quickstart/tutorial (see [Next steps](#next-steps)), you can delete them by doing the following:</span></span>


1. <span data-ttu-id="5c803-210">En el menú izquierdo de Azure Portal, haga clic en **Grupos de recursos** y en **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="5c803-210">From the left-hand menu in the Azure portal, click **Resource groups** and then click **myResourceGroup**.</span></span> 
2. <span data-ttu-id="5c803-211">En la página del grupo de recursos, haga clic en **Eliminar**, escriba **myResourceGroup** en el cuadro de texto y haga clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="5c803-211">On your resource group page, click **Delete**, type **myResourceGroup** in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c803-212">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5c803-212">Next steps</span></span>

<span data-ttu-id="5c803-213">Ahora que tiene una base de datos, puede conectarse y realizar consultas con las herramientas que desee.</span><span class="sxs-lookup"><span data-stu-id="5c803-213">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="5c803-214">Para más información, seleccione una de las herramientas siguientes:</span><span class="sxs-lookup"><span data-stu-id="5c803-214">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="5c803-215">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="5c803-215">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="5c803-216">código de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5c803-216">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="5c803-217">.NET</span><span class="sxs-lookup"><span data-stu-id="5c803-217">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="5c803-218">PHP</span><span class="sxs-lookup"><span data-stu-id="5c803-218">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="5c803-219">Node.js</span><span class="sxs-lookup"><span data-stu-id="5c803-219">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="5c803-220">Java</span><span class="sxs-lookup"><span data-stu-id="5c803-220">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="5c803-221">Python</span><span class="sxs-lookup"><span data-stu-id="5c803-221">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="5c803-222">Ruby</span><span class="sxs-lookup"><span data-stu-id="5c803-222">Ruby</span></span>](sql-database-connect-query-ruby.md)
