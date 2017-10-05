---
title: 'Azure SQL Data Warehouse: tutorial introductorio | Microsoft Docs'
description: "Este tutorial le enseña cómo aprovisionar y cargar datos en Azure SQL Data Warehouse. También aprenderá los conceptos básicos sobre el escalado, la pausa y la optimización."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: barbkess
ms.assetid: 52DFC191-E094-4B04-893F-B64D5828A900
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: quickstart
ms.date: 01/26/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: 95e14824ba3b705bb909ec983652dd3305b98805
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-sql-data-warehouse"></a><span data-ttu-id="3955d-104">Introducción a SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="3955d-104">Get started with SQL Data Warehouse</span></span>

<span data-ttu-id="3955d-105">Este tutorial muestra cómo aprovisionar y cargar datos en Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="3955d-105">This tutorial shows how to provision and load data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="3955d-106">También aprenderá los conceptos básicos sobre el escalado, la pausa y la optimización.</span><span class="sxs-lookup"><span data-stu-id="3955d-106">You’ll also learn the basics about scaling, pausing, and tuning.</span></span> <span data-ttu-id="3955d-107">Cuando haya terminado, estará preparado para consultar y explorar su almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="3955d-107">When you’re finished, you’ll be ready to query and explore your data warehouse.</span></span>

<span data-ttu-id="3955d-108">**Tiempo estimado para completarlo:** se trata de un tutorial completo que incluye código de ejemplo; se tarda aproximadamente 30 minutos en completarlo una vez cumplidos los requisitos previos.</span><span class="sxs-lookup"><span data-stu-id="3955d-108">**Estimated time to complete:** This is an end-to-end tutorial with example code that takes about 30 minutes to complete once you have met the prerequisites.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3955d-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3955d-109">Prerequisites</span></span>

<span data-ttu-id="3955d-110">En el tutorial se da por hecho que está familiarizado con los conceptos básicos de SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="3955d-110">The tutorial assumes you are familiar with SQL Data Warehouse basic concepts.</span></span> <span data-ttu-id="3955d-111">Si necesita una introducción, consulte [¿Qué es SQL Data Warehouse?](sql-data-warehouse-overview-what-is.md)</span><span class="sxs-lookup"><span data-stu-id="3955d-111">If you need an introduction, see [What is SQL Data Warehouse?](sql-data-warehouse-overview-what-is.md)</span></span> 

### <a name="sign-up-for-microsoft-azure"></a><span data-ttu-id="3955d-112">Suscribirse a Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="3955d-112">Sign up for Microsoft Azure</span></span>
<span data-ttu-id="3955d-113">Si no dispone de ninguna cuenta de Microsoft Azure, deberá registrarse para utilizar este servicio.</span><span class="sxs-lookup"><span data-stu-id="3955d-113">If you don't already have a Microsoft Azure account, you need to sign up for one to use this service.</span></span> <span data-ttu-id="3955d-114">Si ya tiene una cuenta, puede omitir este paso.</span><span class="sxs-lookup"><span data-stu-id="3955d-114">If you already have an account, you may skip this step.</span></span> 

1. <span data-ttu-id="3955d-115">Vaya a las páginas de cuentas [https://azure.microsoft.com/account/](https://azure.microsoft.com/account/)</span><span class="sxs-lookup"><span data-stu-id="3955d-115">Navigate to the account pages [https://azure.microsoft.com/account/](https://azure.microsoft.com/account/)</span></span>
2. <span data-ttu-id="3955d-116">Cree una cuenta de Azure gratis o compre una cuenta.</span><span class="sxs-lookup"><span data-stu-id="3955d-116">Create a free Azure account, or purchase an account.</span></span>
3. <span data-ttu-id="3955d-117">Siga las instrucciones.</span><span class="sxs-lookup"><span data-stu-id="3955d-117">Follow the instructions</span></span>

### <a name="install-appropriate-sql-client-drivers-and-tools"></a><span data-ttu-id="3955d-118">Instalación de las herramientas y los controladores del cliente SQL adecuados</span><span class="sxs-lookup"><span data-stu-id="3955d-118">Install appropriate SQL client drivers and tools</span></span>

<span data-ttu-id="3955d-119">La mayoría de las herramientas del cliente SQL se pueden conectar a SQL Data Warehouse mediante JDBC, ODBC o ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="3955d-119">Most SQL client tools can connect to SQL Data Warehouse by using JDBC, ODBC, or ADO.NET.</span></span> <span data-ttu-id="3955d-120">Debido al gran número de características de T-SQL que admite SQL Data Warehouse, algunas aplicaciones cliente no son totalmente compatibles con SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="3955d-120">Due to the large number of T-SQL features that SQL Data Warehouse supports, some client applications are not fully compatible with SQL Data Warehouse.</span></span>

<span data-ttu-id="3955d-121">Si está ejecutando un sistema operativo Windows, se recomienda usar [Visual Studio] o [SQL Server Management Studio].</span><span class="sxs-lookup"><span data-stu-id="3955d-121">If you are running a Windows operating system, we recommend using either [Visual Studio] or [SQL Server Management Studio].</span></span>

[!INCLUDE [Create a new logical server](../../includes/sql-data-warehouse-create-logical-server.md)] 

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="3955d-122">Creación de Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="3955d-122">Create a SQL Data Warehouse</span></span>

<span data-ttu-id="3955d-123">SQL Data Warehouse es un tipo especial de base de datos diseñado para el procesamiento paralelo masivo.</span><span class="sxs-lookup"><span data-stu-id="3955d-123">A SQL Data Warehouse is a special type of database that is designed for massively parallel processing.</span></span> <span data-ttu-id="3955d-124">La base de datos se distribuye en varios nodos y procesa las consultas en paralelo.</span><span class="sxs-lookup"><span data-stu-id="3955d-124">The database is distributed across multiple nodes and processes queries in parallel.</span></span> <span data-ttu-id="3955d-125">SQL Data Warehouse tiene un nodo de control que orquesta las actividades de todos los nodos.</span><span class="sxs-lookup"><span data-stu-id="3955d-125">SQL Data Warehouse has a control node that orchestrates the activities of all the nodes.</span></span> <span data-ttu-id="3955d-126">Los propios nodos usan SQL Database para administrar los datos.</span><span class="sxs-lookup"><span data-stu-id="3955d-126">The nodes themselves use SQL Database to manage your data.</span></span>  

> [!NOTE]
> <span data-ttu-id="3955d-127">La creación de una instancia de Almacenamiento de datos SQL puede dar lugar a un nuevo servicio facturable.</span><span class="sxs-lookup"><span data-stu-id="3955d-127">Creating a SQL Data Warehouse might result in a new billable service.</span></span>  <span data-ttu-id="3955d-128">Para más información, consulte [Precios de Azure SQL Data Warehouse](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="3955d-128">For more information, see [SQL Data Warehouse pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span></span>
>

### <a name="create-a-data-warehouse"></a><span data-ttu-id="3955d-129">Creación del almacenamiento de datos</span><span class="sxs-lookup"><span data-stu-id="3955d-129">Create a data warehouse</span></span>

1. <span data-ttu-id="3955d-130">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3955d-130">Sign into the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3955d-131">Haga clic en **Nuevo** > **Bases de datos** > **SQL Data Warehouse**.</span><span class="sxs-lookup"><span data-stu-id="3955d-131">Click **New** > **Databases** > **SQL Data Warehouse**.</span></span>

    <span data-ttu-id="3955d-132">![NewBlade](../../includes/media/sql-data-warehouse-create-dw/blade-click-new.png) ![SelectDW](../../includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)</span><span class="sxs-lookup"><span data-stu-id="3955d-132">![NewBlade](../../includes/media/sql-data-warehouse-create-dw/blade-click-new.png) ![SelectDW](../../includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)</span></span>

3. <span data-ttu-id="3955d-133">Rellene los detalles de la implementación</span><span class="sxs-lookup"><span data-stu-id="3955d-133">Fill out deployment details</span></span>

    <span data-ttu-id="3955d-134">**Nombre de la base de datos**: elija el que desee.</span><span class="sxs-lookup"><span data-stu-id="3955d-134">**Database Name**: Pick anything you'd like.</span></span> <span data-ttu-id="3955d-135">Si tiene varios almacenamientos de datos, es aconsejable que los nombres incluyan detalles como su región, entorno, etc.; por ejemplo, *mydw-westus-1-test*.</span><span class="sxs-lookup"><span data-stu-id="3955d-135">If you have multiple data warehouses, we recommend your names include details such as the region, environment, for example *mydw-westus-1-test*.</span></span>

    <span data-ttu-id="3955d-136">**Suscripción**: su suscripción a Azure</span><span class="sxs-lookup"><span data-stu-id="3955d-136">**Subscription**: Your Azure subscription</span></span>

    <span data-ttu-id="3955d-137">**Grupo de recursos**: cree un grupo de recursos o seleccione uno existente.</span><span class="sxs-lookup"><span data-stu-id="3955d-137">**Resource Group**: Create a resource group or use an existing resource group.</span></span>
    > [!NOTE]
    > <span data-ttu-id="3955d-138">Los grupos de recursos son útiles para realizar tareas de administración de recursos como el control de acceso y la implementación de plantillas.</span><span class="sxs-lookup"><span data-stu-id="3955d-138">Resource groups are useful for resource administration such as scoping access control and templated deployment.</span></span> <span data-ttu-id="3955d-139">Consulte más información sobre los grupos de recursos de Azure [aquí](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="3955d-139">Read more about Azure resource groups and best practices [here](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)</span></span>

    <span data-ttu-id="3955d-140">**Origen**: base de datos en blanco</span><span class="sxs-lookup"><span data-stu-id="3955d-140">**Source**: Blank Database</span></span>

    <span data-ttu-id="3955d-141">**Servidor**: seleccione el servidor que creó en los [requisitos previos].</span><span class="sxs-lookup"><span data-stu-id="3955d-141">**Server**: Select the server you created in [Prerequisites].</span></span>

    <span data-ttu-id="3955d-142">**Intercalación**: mantenga la intercalación predeterminada: SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="3955d-142">**Collation**: Leave the default collation SQL_Latin1_General_CP1_CI_AS.</span></span>

    <span data-ttu-id="3955d-143">**Select performance** (Seleccionar rendimiento): se recomienda mantener el estándar 400DWU.</span><span class="sxs-lookup"><span data-stu-id="3955d-143">**Select performance**: We recommend starting with the standard 400DWU.</span></span>

4. <span data-ttu-id="3955d-144">Seleccione **Anclar al panel**![Anclar al panel](./media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)</span><span class="sxs-lookup"><span data-stu-id="3955d-144">Choose **Pin to dashboard** ![Pin To Dashboard](./media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)</span></span>

5. <span data-ttu-id="3955d-145">Póngase cómodo y espere a que el almacenamiento de datos se implemente.</span><span class="sxs-lookup"><span data-stu-id="3955d-145">Sit back and wait for your data warehouse to deploy!</span></span> <span data-ttu-id="3955d-146">Lo normal es que este proceso tarde varios minutos.</span><span class="sxs-lookup"><span data-stu-id="3955d-146">It's normal for this process to take several minutes.</span></span> <span data-ttu-id="3955d-147">El portal le avisa cuando está el almacenamiento de datos está listo para usarse.</span><span class="sxs-lookup"><span data-stu-id="3955d-147">The portal notifies you when your data warehouse is ready to use.</span></span> 

## <a name="connect-to-sql-data-warehouse"></a><span data-ttu-id="3955d-148">Conexión a Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="3955d-148">Connect to SQL Data Warehouse</span></span>

<span data-ttu-id="3955d-149">Este tutorial usa SQL Server Management Studio (SSMS) para conectarse al almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="3955d-149">This tutorial uses SQL Server Management Studio (SSMS) to connect to the data warehouse.</span></span> <span data-ttu-id="3955d-150">Puede conectarse a SQL Data Warehouse a través de los siguientes conectores compatibles: ADO.NET, JDBC, ODBC y PHP.</span><span class="sxs-lookup"><span data-stu-id="3955d-150">You can connect to SQL Data Warehouse through these supported connectors: ADO.NET, JDBC, ODBC, and PHP.</span></span> <span data-ttu-id="3955d-151">Recuerde que la funcionalidad podría ser limitada para herramientas no compatibles con Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3955d-151">Remember, functionality might be limited for tools that are not supported by Microsoft.</span></span>


### <a name="get-connection-information"></a><span data-ttu-id="3955d-152">Obtención de información sobre la conexión</span><span class="sxs-lookup"><span data-stu-id="3955d-152">Get connection information</span></span>

<span data-ttu-id="3955d-153">Para conectarse a su almacenamiento de datos, debe conectarse mediante el servidor lógico de SQL Server que creó en los [requisitos previos].</span><span class="sxs-lookup"><span data-stu-id="3955d-153">To connect to your data warehouse, you need to connect through the logical SQL server you created in [Prerequisites].</span></span>

1. <span data-ttu-id="3955d-154">Seleccione su almacenamiento de datos en el panel o búsquelo en los recursos.</span><span class="sxs-lookup"><span data-stu-id="3955d-154">Select your data warehouse from the dashboard or search for it in your resources.</span></span>

    ![Panel de SQL Data Warehouse](./media/sql-data-warehouse-get-started-tutorial/sql-dw-dashboard.png)

2. <span data-ttu-id="3955d-156">Busque el nombre completo del servidor lógico de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3955d-156">Find the full name for the logical SQL server.</span></span>

    ![Seleccionar nombre del servidor](./media/sql-data-warehouse-get-started-tutorial/select-server.png)

3. <span data-ttu-id="3955d-158">Abra SSMS y utilice el explorador de objetos para conectarse a este servidor con las credenciales del administrador del servidor que creó en los [requisitos previos].</span><span class="sxs-lookup"><span data-stu-id="3955d-158">Open SSMS and use object explorer to connect to this server using the server admin credentials you created in [Prerequisites]</span></span>

    ![Conectarse con SSMS](./media/sql-data-warehouse-get-started-tutorial/ssms-connect.png)

<span data-ttu-id="3955d-160">Si todo funciona correctamente, ahora deberá estar conectado al servidor lógico de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3955d-160">If all goes correctly, you should now be connected to your logical SQL server.</span></span> <span data-ttu-id="3955d-161">Puesto que ha iniciado sesión como administrador del servidor, puede conectarse a cualquier base de datos hospedada por el servidor, incluida la base de datos maestra.</span><span class="sxs-lookup"><span data-stu-id="3955d-161">Since you logged in as the server admin, you can connect to any database hosted by the server, including the master database.</span></span> 

<span data-ttu-id="3955d-162">Solo hay una cuenta de administrador en el servidor, y tiene más privilegios de cualquier usuario.</span><span class="sxs-lookup"><span data-stu-id="3955d-162">There is only one server admin account and it has the most privileges of any user.</span></span> <span data-ttu-id="3955d-163">Tenga cuidado de no permitir que demasiadas personas de su organización conozcan la contraseña de administrador.</span><span class="sxs-lookup"><span data-stu-id="3955d-163">Be careful not to allow too many people in your organization to know the admin password.</span></span> 

<span data-ttu-id="3955d-164">También puede tener una cuenta de administrador de Azure Active Directory,</span><span class="sxs-lookup"><span data-stu-id="3955d-164">You can also have an Azure active directory admin account.</span></span> <span data-ttu-id="3955d-165">pero no proporcionamos los detalles aquí.</span><span class="sxs-lookup"><span data-stu-id="3955d-165">We don't provide the details here.</span></span> <span data-ttu-id="3955d-166">Si desea más información acerca del uso de autenticación de Azure Active Directory, consulte [Autenticación de Azure AD](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).</span><span class="sxs-lookup"><span data-stu-id="3955d-166">If you want to learn more about using Azure Active Directory authentication, see [Azure AD authentication](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).</span></span>

<span data-ttu-id="3955d-167">A continuación, veremos la creación de usuarios e inicios de sesión adicionales.</span><span class="sxs-lookup"><span data-stu-id="3955d-167">Next, we explore creating additional logins and users.</span></span>


## <a name="create-a-database-user"></a><span data-ttu-id="3955d-168">Creación de un usuario de base de datos</span><span class="sxs-lookup"><span data-stu-id="3955d-168">Create a database user</span></span>

<span data-ttu-id="3955d-169">En este paso, creará una cuenta de usuario para acceder a su almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="3955d-169">In this step, you create a user account to access your data warehouse.</span></span> <span data-ttu-id="3955d-170">También le mostramos cómo otorgar a ese usuario la capacidad de ejecutar consultas con una gran cantidad de memoria y recursos de CPU.</span><span class="sxs-lookup"><span data-stu-id="3955d-170">We also show you how to give that user the ability to run queries with a large amount of memory and CPU resources.</span></span>

### <a name="notes-about-resource-classes-for-allocating-resources-to-queries"></a><span data-ttu-id="3955d-171">Notas acerca de las clases de recursos para asignar recursos a las consultas</span><span class="sxs-lookup"><span data-stu-id="3955d-171">Notes about resource classes for allocating resources to queries</span></span>

- <span data-ttu-id="3955d-172">Para mantener los datos seguros, no use la cuenta de administrador del servidor para ejecutar consultas en las bases de datos de producción.</span><span class="sxs-lookup"><span data-stu-id="3955d-172">To keep your data safe, don't use the server admin to run queries on your production databases.</span></span> <span data-ttu-id="3955d-173">Tiene más privilegios que cualquier usuario y usarlo para realizar operaciones en los datos de usuario pone los datos en peligro.</span><span class="sxs-lookup"><span data-stu-id="3955d-173">It has the most privileges of any user and using it to perform operations on user data puts your data at risk.</span></span> <span data-ttu-id="3955d-174">Además, puesto que el administrador del servidor se ha diseñado para realizar operaciones de administración, ejecuta operaciones con solo una pequeña asignación de memoria y recursos de CPU.</span><span class="sxs-lookup"><span data-stu-id="3955d-174">Also, since the server admin is meant to perform management operations, it runs operations with only a small allocation of memory and CPU resources.</span></span> 

- <span data-ttu-id="3955d-175">SQL Data Warehouse usa roles de base de datos predefinidos, llamados clases de recursos, para asignar diferentes cantidades de memoria, recursos de CPU y espacios de simultaneidad a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="3955d-175">SQL Data Warehouse uses pre-defined database roles, called resource classes, to allocate different amounts of memory, CPU resources, and concurrency slots to users.</span></span> <span data-ttu-id="3955d-176">Cada usuario puede pertenecer a una clase de recursos pequeña, mediana, grande o extragrande.</span><span class="sxs-lookup"><span data-stu-id="3955d-176">Each user can belong to a small, medium, large, or extra-large resource class.</span></span> <span data-ttu-id="3955d-177">La clase de recurso del usuario determina los recursos que tiene el usuario para ejecutar consultas y operaciones de carga.</span><span class="sxs-lookup"><span data-stu-id="3955d-177">The user's resource class determines the resources the user has to run queries and load operations.</span></span>

- <span data-ttu-id="3955d-178">Para lograr una compresión de datos óptima, es posible que el usuario necesite realizar cargas con asignaciones de recursos grandes o extragrandes.</span><span class="sxs-lookup"><span data-stu-id="3955d-178">For optimal data compression, the user may need to load with large or extra large resource allocations.</span></span> <span data-ttu-id="3955d-179">Obtenga más información sobre las clases de recursos [aquí](./sql-data-warehouse-develop-concurrency.md#resource-classes):</span><span class="sxs-lookup"><span data-stu-id="3955d-179">Read more about resource classes [here](./sql-data-warehouse-develop-concurrency.md#resource-classes):</span></span>

### <a name="create-an-account-that-can-control-a-database"></a><span data-ttu-id="3955d-180">Creación de una cuenta que puede controlar una base de datos</span><span class="sxs-lookup"><span data-stu-id="3955d-180">Create an account that can control a database</span></span>

<span data-ttu-id="3955d-181">Puesto que ha iniciado sesión como administrador del servidor, tiene permisos para crear inicios de sesión y usuarios.</span><span class="sxs-lookup"><span data-stu-id="3955d-181">Since you are currently logged in as the server admin you have permissions to create logins and users.</span></span>

1. <span data-ttu-id="3955d-182">Con SSMS u otro cliente de consulta, abra una nueva consulta para **master**.</span><span class="sxs-lookup"><span data-stu-id="3955d-182">Using SSMS or another query client, open a new query for **master**.</span></span>

    ![Nueva consulta en Master](./media/sql-data-warehouse-get-started-tutorial/query-on-server.png)

    ![Nueva consulta en Master1](./media/sql-data-warehouse-get-started-tutorial/query-on-master.png)

2. <span data-ttu-id="3955d-185">En la ventana de consulta, ejecute este comando T-SQL para crear un inicio de sesión llamado MedRCLogin y un usuario llamado LoadingUser.</span><span class="sxs-lookup"><span data-stu-id="3955d-185">In the query window, run this T-SQL command to create a login named MedRCLogin and user named LoadingUser.</span></span> <span data-ttu-id="3955d-186">Este inicio de sesión puede conectarse al servidor lógico de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3955d-186">This login can connect to the logical SQL server.</span></span>

    ```sql
    CREATE LOGIN MedRCLogin WITH PASSWORD = 'a123reallySTRONGpassword!';
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

3. <span data-ttu-id="3955d-187">Ahora, consultando la *base de datos de SQL Data Warehouse*, cree un usuario de base de datos basado en el inicio de sesión que creó para acceder a la base de datos y realizar operaciones en ella.</span><span class="sxs-lookup"><span data-stu-id="3955d-187">Now querying the *SQL Data Warehouse database*, create a database user based on the login you created to access and perform operations on the database.</span></span>

    ```sql
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

4. <span data-ttu-id="3955d-188">Conceda permisos de control de usuario para la base de datos NYT.</span><span class="sxs-lookup"><span data-stu-id="3955d-188">Give the database user control permissions to the database called NYT.</span></span> 

    ```sql
    GRANT CONTROL ON DATABASE::[NYT] to LoadingUser;
    ```
    > [!NOTE]
    > <span data-ttu-id="3955d-189">Si el nombre de la base de datos contiene guiones asegúrese de incluirlo entre corchetes.</span><span class="sxs-lookup"><span data-stu-id="3955d-189">If your database name has hyphens in it, be sure to wrap it in brackets!</span></span> 
    >

### <a name="give-the-user-medium-resource-allocations"></a><span data-ttu-id="3955d-190">Asignaciones de recursos de tamaño medio al usuario</span><span class="sxs-lookup"><span data-stu-id="3955d-190">Give the user medium resource allocations</span></span>

1. <span data-ttu-id="3955d-191">Ejecute este comando T-SQL para convertirlo en miembro de la clase de recursos de tamaño medio, denominada mediumrc.</span><span class="sxs-lookup"><span data-stu-id="3955d-191">Run this T-SQL command to make it a member of the medium resource class, which is called mediumrc.</span></span> 

    ```sql
    EXEC sp_addrolemember 'mediumrc', 'LoadingUser';
    ```
    > [!NOTE]
    > <span data-ttu-id="3955d-192">Haga clic [aquí](sql-data-warehouse-develop-concurrency.md#resource-classes) para más información sobre las clases de simultaneidad y recursos.</span><span class="sxs-lookup"><span data-stu-id="3955d-192">Click [here](sql-data-warehouse-develop-concurrency.md#resource-classes) to learn more about concurrency and resource classes!</span></span> 
    >

2. <span data-ttu-id="3955d-193">Conexión al servidor lógico con las nuevas credenciales</span><span class="sxs-lookup"><span data-stu-id="3955d-193">Connect to the logical server with the new credentials</span></span>

    ![Inicie sesión con el nuevo inicio de sesión](./media/sql-data-warehouse-get-started-tutorial/new-login.png)


## <a name="load-data-from-azure-blob-storage"></a><span data-ttu-id="3955d-195">Carga de datos del almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="3955d-195">Load data from Azure blob storage</span></span>

<span data-ttu-id="3955d-196">Ahora está listo para cargar datos en el almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="3955d-196">You are now ready to load data into your data warehouse.</span></span> <span data-ttu-id="3955d-197">Este paso muestra cómo cargar datos de los taxis de Nueva York procedentes de una instancia de Azure Storage Blob público.</span><span class="sxs-lookup"><span data-stu-id="3955d-197">This step shows you how to load New York City taxi cab data from a public Azure storage blob.</span></span> 

- <span data-ttu-id="3955d-198">Una forma habitual de cargar datos en SQL Data Warehouse es mover los datos a Azure Blob Storage y, después, cargarlos en su almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="3955d-198">A common way to load data into SQL Data Warehouse is to first move the data to Azure blob storage, and then load it into your data warehouse.</span></span> <span data-ttu-id="3955d-199">Para que sea más fácil entender cómo se realiza la carga, tenemos datos de los taxis de Nueva York ya hospedados en una instancia de Azure Storage Blob público.</span><span class="sxs-lookup"><span data-stu-id="3955d-199">To make it easier to understand how to load, we have New York taxi cab data already hosted in a public Azure storage blob.</span></span> 

- <span data-ttu-id="3955d-200">Para consultas futuras y aprender cómo obtener los datos en Azure Blob Storage o cómo cargarlos directamente desde el origen en SQL Data Warehouse, consulte la [introducción a la carga](sql-data-warehouse-overview-load.md).</span><span class="sxs-lookup"><span data-stu-id="3955d-200">For future reference, to learn how to get your data to Azure blob storage or to load it directly from your source into SQL Data Warehouse, see the [loading overview](sql-data-warehouse-overview-load.md).</span></span>


### <a name="define-external-data"></a><span data-ttu-id="3955d-201">Definición de datos externos</span><span class="sxs-lookup"><span data-stu-id="3955d-201">Define external data</span></span>

1. <span data-ttu-id="3955d-202">Cree una clave maestra.</span><span class="sxs-lookup"><span data-stu-id="3955d-202">Create a master key.</span></span> <span data-ttu-id="3955d-203">Solo necesita crear una clave maestra una vez para cada base de datos.</span><span class="sxs-lookup"><span data-stu-id="3955d-203">You only need to create a master key once per database.</span></span> 

    ```sql
    CREATE MASTER KEY;
    ```

2. <span data-ttu-id="3955d-204">Defina la ubicación del blob de Azure que contiene los datos de los taxis.</span><span class="sxs-lookup"><span data-stu-id="3955d-204">Define the location of the Azure blob that contains the taxi cab data.</span></span>  

    ```sql
    CREATE EXTERNAL DATA SOURCE NYTPublic
    WITH
    (
        TYPE = Hadoop,
        LOCATION = 'wasbs://2013@nytpublic.blob.core.windows.net/'
    );
    ```

3. <span data-ttu-id="3955d-205">Definición de los formatos de archivo externos</span><span class="sxs-lookup"><span data-stu-id="3955d-205">Define the external file formats</span></span>

    <span data-ttu-id="3955d-206">El comando ```CREATE EXTERNAL FILE FORMAT``` se utiliza para especificar el formato de los archivos que contienen los datos externos.</span><span class="sxs-lookup"><span data-stu-id="3955d-206">The ```CREATE EXTERNAL FILE FORMAT``` command is used to specify the format of files that contain the external data.</span></span> <span data-ttu-id="3955d-207">Dichos archivos contienen texto separado por uno o más caracteres, denominados delimitadores.</span><span class="sxs-lookup"><span data-stu-id="3955d-207">They contain text separated by one or more characters called delimiters.</span></span> <span data-ttu-id="3955d-208">Con fines de demostración, los datos de los taxis se almacenan como datos sin comprimir y como datos comprimidos con gzip.</span><span class="sxs-lookup"><span data-stu-id="3955d-208">For demonstration purposes, the taxi cab data is stored both as uncompressed data and as gzip compressed data.</span></span>

    <span data-ttu-id="3955d-209">Ejecute estos comandos T-SQL para definir dos formatos diferentes: sin comprimir y comprimido.</span><span class="sxs-lookup"><span data-stu-id="3955d-209">Run these T-SQL commands to define two different formats: uncompressed and compressed.</span></span>

    ```sql
    CREATE EXTERNAL FILE FORMAT uncompressedcsv
    WITH (
        FORMAT_TYPE = DELIMITEDTEXT,
        FORMAT_OPTIONS ( 
            FIELD_TERMINATOR = ',',
            STRING_DELIMITER = '',
            DATE_FORMAT = '',
            USE_TYPE_DEFAULT = False
        )
    );

    CREATE EXTERNAL FILE FORMAT compressedcsv
    WITH ( 
        FORMAT_TYPE = DELIMITEDTEXT,
        FORMAT_OPTIONS ( FIELD_TERMINATOR = '|',
            STRING_DELIMITER = '',
        DATE_FORMAT = '',
            USE_TYPE_DEFAULT = False
        ),
        DATA_COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'
    );
    ```

4.  <span data-ttu-id="3955d-210">Cree un esquema para el formato de archivos externos.</span><span class="sxs-lookup"><span data-stu-id="3955d-210">Create a schema for your external file format.</span></span> 

    ```sql
    CREATE SCHEMA ext;
    ```
5. <span data-ttu-id="3955d-211">Creación de la tablas externas</span><span class="sxs-lookup"><span data-stu-id="3955d-211">Create the external tables.</span></span> <span data-ttu-id="3955d-212">Estas tablas hacen referencia a los datos almacenados en Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="3955d-212">These tables reference data stored in Azure blob storage.</span></span> <span data-ttu-id="3955d-213">Ejecute los siguientes comandos T-SQL para crear varias tablas externas que apuntan al blob de Azure que hemos definido previamente en nuestro origen de datos externo.</span><span class="sxs-lookup"><span data-stu-id="3955d-213">Run the following T-SQL commands to create several external tables that all point to the Azure blob we defined previously in our external data source.</span></span>

```sql
    CREATE EXTERNAL TABLE [ext].[Date] 
    (
        [DateID] int NOT NULL,
        [Date] datetime NULL,
        [DateBKey] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DaySuffix] varchar(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeek] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeekInMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeekInYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfQuarter] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfYear] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfMonth] varchar(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Month] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Quarter] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [QuarterName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Year] char(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [YearName] char(7) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthYear] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MMYYYY] char(6) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [FirstDayOfMonth] date NULL,
        [LastDayOfMonth] date NULL,
        [FirstDayOfQuarter] date NULL,
        [LastDayOfQuarter] date NULL,
        [FirstDayOfYear] date NULL,
        [LastDayOfYear] date NULL,
        [IsHolidayUSA] bit NULL,
        [IsWeekday] bit NULL,
        [HolidayUSA] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Date',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    );
    
    CREATE EXTERNAL TABLE [ext].[Geography]
    (
        [GeographyID] int NOT NULL,
        [ZipCodeBKey] varchar(10) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [County] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [City] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [State] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Country] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [ZipCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Geography',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0 
    );
        
    
    CREATE EXTERNAL TABLE [ext].[HackneyLicense]
    (
        [HackneyLicenseID] int NOT NULL,
        [HackneyLicenseBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [HackneyLicenseCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'HackneyLicense',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
        
    
    CREATE EXTERNAL TABLE [ext].[Medallion]
    (
        [MedallionID] int NOT NULL,
        [MedallionBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [MedallionCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Medallion',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
        
    CREATE EXTERNAL TABLE [ext].[Time]
    (
        [TimeID] int NOT NULL,
        [TimeBKey] varchar(8) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [HourNumber] tinyint NOT NULL,
        [MinuteNumber] tinyint NOT NULL,
        [SecondNumber] tinyint NOT NULL,
        [TimeInSecond] int NOT NULL,
        [HourlyBucket] varchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [DayTimeBucketGroupKey] int NOT NULL,
        [DayTimeBucket] varchar(100) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL
    )
    WITH
    (
        LOCATION = 'Time',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
    
    
    CREATE EXTERNAL TABLE [ext].[Trip]
    (
        [DateID] int NOT NULL,
        [MedallionID] int NOT NULL,
        [HackneyLicenseID] int NOT NULL,
        [PickupTimeID] int NOT NULL,
        [DropoffTimeID] int NOT NULL,
        [PickupGeographyID] int NULL,
        [DropoffGeographyID] int NULL,
        [PickupLatitude] float NULL,
        [PickupLongitude] float NULL,
        [PickupLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DropoffLatitude] float NULL,
        [DropoffLongitude] float NULL,
        [DropoffLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [PassengerCount] int NULL,
        [TripDurationSeconds] int NULL,
        [TripDistanceMiles] float NULL,
        [PaymentType] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [FareAmount] money NULL,
        [SurchargeAmount] money NULL,
        [TaxAmount] money NULL,
        [TipAmount] money NULL,
        [TollsAmount] money NULL,
        [TotalAmount] money NULL
    )
    WITH
    (
        LOCATION = 'Trip2013',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = compressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
    
    CREATE EXTERNAL TABLE [ext].[Weather]
    (
        [DateID] int NOT NULL,
        [GeographyID] int NOT NULL,
        [PrecipitationInches] float NOT NULL,
        [AvgTemperatureFahrenheit] float NOT NULL
    )
    WITH
    (
        LOCATION = 'Weather2013',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
```

### <a name="import-the-data-from-azure-blob-storage"></a><span data-ttu-id="3955d-214">Importe los datos desde Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="3955d-214">Import the data from Azure blob storage.</span></span>

<span data-ttu-id="3955d-215">SQL Data Warehouse admite una instrucción clave denominada CREATE TABLE AS SELECT (CTAS).</span><span class="sxs-lookup"><span data-stu-id="3955d-215">SQL Data Warehouse supports a key statement called CREATE TABLE AS SELECT (CTAS).</span></span> <span data-ttu-id="3955d-216">Esta instrucción crea una nueva tabla en función de los resultados de una instrucción select.</span><span class="sxs-lookup"><span data-stu-id="3955d-216">This statement creates a new table based on the results of a select statement.</span></span> <span data-ttu-id="3955d-217">La nueva tabla tiene las mismas columnas y los mismos tipos de datos que los resultados de la instrucción select.</span><span class="sxs-lookup"><span data-stu-id="3955d-217">The new table has the same columns and data types as the results of the select statement.</span></span>  <span data-ttu-id="3955d-218">Es una manera elegante de importar datos de Azure Blob Storage en SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="3955d-218">This is an elegant way to import data from Azure blob storage into SQL Data Warehouse.</span></span>

1. <span data-ttu-id="3955d-219">Ejecute este script para importar los datos.</span><span class="sxs-lookup"><span data-stu-id="3955d-219">Run this script to import your data.</span></span>

    ```sql
    CREATE TABLE [dbo].[Date]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Date]
    OPTION (LABEL = 'CTAS : Load [dbo].[Date]')
    ;
    
    CREATE TABLE [dbo].[Geography]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS
    SELECT * FROM [ext].[Geography]
    OPTION (LABEL = 'CTAS : Load [dbo].[Geography]')
    ;
    
    CREATE TABLE [dbo].[HackneyLicense]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[HackneyLicense]
    OPTION (LABEL = 'CTAS : Load [dbo].[HackneyLicense]')
    ;
    
    CREATE TABLE [dbo].[Medallion]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Medallion]
    OPTION (LABEL = 'CTAS : Load [dbo].[Medallion]')
    ;
    
    CREATE TABLE [dbo].[Time]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Time]
    OPTION (LABEL = 'CTAS : Load [dbo].[Time]')
    ;
    
    CREATE TABLE [dbo].[Weather]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Weather]
    OPTION (LABEL = 'CTAS : Load [dbo].[Weather]')
    ;
    
    CREATE TABLE [dbo].[Trip]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Trip]
    OPTION (LABEL = 'CTAS : Load [dbo].[Trip]')
    ;
    ```

2. <span data-ttu-id="3955d-220">Consulte los datos mientras se carga.</span><span class="sxs-lookup"><span data-stu-id="3955d-220">View your data as it loads.</span></span>

   <span data-ttu-id="3955d-221">Está cargando varios gigabytes de datos y comprimiéndolos en índices de almacén de columnas en clúster de alto rendimiento.</span><span class="sxs-lookup"><span data-stu-id="3955d-221">You’re loading several GBs of data and compressing it into highly performant clustered columnstore indexes.</span></span> <span data-ttu-id="3955d-222">Ejecute la siguiente consulta, que usa vistas de administración dinámica (DMV) para mostrar el estado de la carga.</span><span class="sxs-lookup"><span data-stu-id="3955d-222">Run the following query that uses a dynamic management views (DMVs) to show the status of the load.</span></span> <span data-ttu-id="3955d-223">Después de iniciar la consulta, tómese un café y coma algo mientras SQL Data Warehouse hace el trabajo duro.</span><span class="sxs-lookup"><span data-stu-id="3955d-223">After starting the query, grab a coffee and a snack while SQL Data Warehouse does some heavy lifting.</span></span>
    
    ```sql
    SELECT
        r.command,
        s.request_id,
        r.status,
        count(distinct input_name) as nbr_files,
        sum(s.bytes_processed)/1024/1024/1024 as gb_processed
    FROM 
        sys.dm_pdw_exec_requests r
        INNER JOIN sys.dm_pdw_dms_external_work s
        ON r.request_id = s.request_id
    WHERE
        r.[label] = 'CTAS : Load [dbo].[Date]' OR
        r.[label] = 'CTAS : Load [dbo].[Geography]' OR
        r.[label] = 'CTAS : Load [dbo].[HackneyLicense]' OR
        r.[label] = 'CTAS : Load [dbo].[Medallion]' OR
        r.[label] = 'CTAS : Load [dbo].[Time]' OR
        r.[label] = 'CTAS : Load [dbo].[Weather]' OR
        r.[label] = 'CTAS : Load [dbo].[Trip]'
    GROUP BY
        r.command,
        s.request_id,
        r.status
    ORDER BY
        nbr_files desc, 
        gb_processed desc;
    ```

3. <span data-ttu-id="3955d-224">Consulte todas las consultas del sistema.</span><span class="sxs-lookup"><span data-stu-id="3955d-224">View all system queries.</span></span>

    ```sql
    SELECT * FROM sys.dm_pdw_exec_requests;
    ```

4. <span data-ttu-id="3955d-225">Disfrute viendo cómo los datos se cargan ordenadamente en Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="3955d-225">Enjoy seeing your data nicely loaded into your Azure SQL Data Warehouse.</span></span>

    ![Consulte los datos cargados](./media/sql-data-warehouse-get-started-tutorial/see-data-loaded.png)


## <a name="improve-query-performance"></a><span data-ttu-id="3955d-227">Mejora del rendimiento de las consultas</span><span class="sxs-lookup"><span data-stu-id="3955d-227">Improve query performance</span></span>

<span data-ttu-id="3955d-228">Hay varias maneras de mejorar el rendimiento de las consultas y de lograr el rendimiento de alta velocidad que el diseño de SQL Data Warehouse ofrece.</span><span class="sxs-lookup"><span data-stu-id="3955d-228">There are several ways to improve query performance and to achieve the high-speed performance that SQL Data Warehouse is designed to provide.</span></span>  

### <a name="see-the-effect-of-scaling-on-query-performance"></a><span data-ttu-id="3955d-229">Visualización del efecto del escalado en el rendimiento de las consultas</span><span class="sxs-lookup"><span data-stu-id="3955d-229">See the effect of scaling on query performance</span></span> 

<span data-ttu-id="3955d-230">Una manera de mejorar el rendimiento de las consultas es escalar los recursos cambiando el nivel de servicio de DWU para el almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="3955d-230">One way to improve query performance is to scale resources by changing the DWU service level for your data warehouse.</span></span> <span data-ttu-id="3955d-231">Cada nivel de servicio cuesta más que el anterior, pero se puede reducir la escala o pausar recursos en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="3955d-231">Each service level costs more, but you can scale back or pause resources at any time.</span></span> 

<span data-ttu-id="3955d-232">En este paso se compara el rendimiento de dos configuraciones de DWU distintas.</span><span class="sxs-lookup"><span data-stu-id="3955d-232">In this step, you compare performance at two different DWU settings.</span></span>

<span data-ttu-id="3955d-233">Primero vamos a reducir verticalmente hasta 100 DWU para que hacernos una idea del rendimiento de los nodos de proceso por separado.</span><span class="sxs-lookup"><span data-stu-id="3955d-233">First, let's scale the sizing down to 100 DWU so we can get an idea of how one compute node might perform on its own.</span></span>

1. <span data-ttu-id="3955d-234">Vaya al portal y seleccione la instancia de SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="3955d-234">Go to the portal and select your SQL Data Warehouse.</span></span>

2. <span data-ttu-id="3955d-235">Seleccione la escala en la hoja SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="3955d-235">Select scale in the SQL Data Warehouse blade.</span></span> 

    ![Escalado de Data Warehouse desde el portal](./media/sql-data-warehouse-get-started-tutorial/scale-dw.png)

3. <span data-ttu-id="3955d-237">Reduzca el rendimiento mediante la barra a 100 DWU y pulse Guardar.</span><span class="sxs-lookup"><span data-stu-id="3955d-237">Scale down the performance bar to 100 DWU and hit save.</span></span>

    ![Escalar y guardar](./media/sql-data-warehouse-get-started-tutorial/scale-and-save.png)

4. <span data-ttu-id="3955d-239">Espere a que finalice su operación de escalado.</span><span class="sxs-lookup"><span data-stu-id="3955d-239">Wait for your scale operation to finish.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3955d-240">No se pueden ejecutar consultas mientras se cambia la escala.</span><span class="sxs-lookup"><span data-stu-id="3955d-240">Queries cannot run while changing the scale.</span></span> <span data-ttu-id="3955d-241">El escalado **elimina** las consultas actualmente en ejecución.</span><span class="sxs-lookup"><span data-stu-id="3955d-241">Scaling **kills** your currently running queries.</span></span> <span data-ttu-id="3955d-242">Puede reiniciarlas una vez finalizada la operación.</span><span class="sxs-lookup"><span data-stu-id="3955d-242">You can restart them when the operation is finished.</span></span>
    >
    
5. <span data-ttu-id="3955d-243">Realice un examen de los datos de los trayectos y seleccione el primer millón de entradas de todas las columnas.</span><span class="sxs-lookup"><span data-stu-id="3955d-243">Do a scan operation on the trip data, selecting the top million entries for all the columns.</span></span> <span data-ttu-id="3955d-244">Si desea avanzar rápidamente, seleccione menos filas.</span><span class="sxs-lookup"><span data-stu-id="3955d-244">If you're eager to move on quickly, feel free to select fewer rows.</span></span> <span data-ttu-id="3955d-245">Tome nota del tiempo que tarda esta operación en ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="3955d-245">Take note of the time it takes to run this operation.</span></span>

    ```sql
    SELECT TOP(1000000) * FROM dbo.[Trip]
    ```
6. <span data-ttu-id="3955d-246">Escale el almacenamiento de datos de nuevo a 400 DWU.</span><span class="sxs-lookup"><span data-stu-id="3955d-246">Scale your data warehouse back to 400 DWU.</span></span> <span data-ttu-id="3955d-247">Tenga en cuenta que cada 100 DWU se agrega otro nodo de proceso a Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="3955d-247">Remember, each 100 DWU is adding another compute node to your Azure SQL Data Warehouse.</span></span>

7. <span data-ttu-id="3955d-248">Ejecute la consulta de nuevo.</span><span class="sxs-lookup"><span data-stu-id="3955d-248">Run the query again!</span></span> <span data-ttu-id="3955d-249">Debe observar una diferencia significativa.</span><span class="sxs-lookup"><span data-stu-id="3955d-249">You should notice a significant difference.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="3955d-250">Dado que la consulta devuelve una gran cantidad de datos, la disponibilidad de ancho de banda de la máquina que ejecute SSMS puede verse afectada por un cuello de botella en el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="3955d-250">Because the query returns a lot of data, the bandwidth availability of the machine running SSMS may be a performance bottleneck.</span></span> <span data-ttu-id="3955d-251">Como consecuencia, es posible que no pueda ver ninguna mejora del rendimiento.</span><span class="sxs-lookup"><span data-stu-id="3955d-251">This can result in you not seeing any performance improvements!</span></span>

> [!NOTE]
> <span data-ttu-id="3955d-252">Como SQL Data Warehouse utiliza el procesamiento paralelo masivo,</span><span class="sxs-lookup"><span data-stu-id="3955d-252">Since SQL Data Warehouse uses massively parallel processing.</span></span> <span data-ttu-id="3955d-253">las consultas que examinen o realicen funciones analíticas en millones de filas experimentarán la auténtica potencia de Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="3955d-253">Queries that scan or perform analytic functions on millions of rows experience the true power of Azure SQL Data Warehouse.</span></span>
>

### <a name="see-the-effect-of-statistics-on-query-performance"></a><span data-ttu-id="3955d-254">Visualización del efecto de las estadísticas en el rendimiento de las consultas</span><span class="sxs-lookup"><span data-stu-id="3955d-254">See the effect of statistics on query performance</span></span>

1. <span data-ttu-id="3955d-255">Ejecute una consulta que combine la tabla Date (Fecha) con la tabla Trip (Trayecto)</span><span class="sxs-lookup"><span data-stu-id="3955d-255">Run a query that joins the Date table with the Trip table</span></span>

    ```sql
    SELECT TOP (1000000) 
        dt.[DayOfWeek],
        tr.[MedallionID],
        tr.[HackneyLicenseID],
        tr.[PickupTimeID],
        tr.[DropoffTimeID],
        tr.[PickupGeographyID],
        tr.[DropoffGeographyID],
        tr.[PickupLatitude],
        tr.[PickupLongitude],
        tr.[PickupLatLong],
        tr.[DropoffLatitude],
        tr.[DropoffLongitude],
        tr.[DropoffLatLong],
        tr.[PassengerCount],
        tr.[TripDurationSeconds],
        tr.[TripDistanceMiles],
        tr.[PaymentType],
        tr.[FareAmount],
        tr.[SurchargeAmount],
        tr.[TaxAmount],
        tr.[TipAmount],
        tr.[TollsAmount],
        tr.[TotalAmount]
    FROM [dbo].[Trip] as tr
        JOIN dbo.[Date] as dt
        ON  tr.DateID = dt.DateID
    ```

    <span data-ttu-id="3955d-256">Esta consulta tarda algún tiempo, ya que SQL Data Warehouse tiene que distribuir aleatoriamente los datos para la combinación.</span><span class="sxs-lookup"><span data-stu-id="3955d-256">This query takes a while because SQL Data Warehouse has to shuffle data before it can perform the join.</span></span> <span data-ttu-id="3955d-257">Las combinaciones no necesitan la distribución aleatoria de los datos si están diseñadas para unirlos de la misma manera en la que se distribuyen.</span><span class="sxs-lookup"><span data-stu-id="3955d-257">Joins do not have to shuffle data if they are designed to join data in the same way it is distributed.</span></span> <span data-ttu-id="3955d-258">Esto es un asunto más complicado.</span><span class="sxs-lookup"><span data-stu-id="3955d-258">That's a deeper subject.</span></span> 

2. <span data-ttu-id="3955d-259">Las estadísticas marcan la diferencia.</span><span class="sxs-lookup"><span data-stu-id="3955d-259">Statistics make a difference.</span></span> 
3. <span data-ttu-id="3955d-260">Ejecute esta instrucción para crear estadísticas en las columnas de combinación.</span><span class="sxs-lookup"><span data-stu-id="3955d-260">Run this statement to create statistics on the join columns.</span></span>

    ```sql
    CREATE STATISTICS [dbo.Date DateID stats] ON dbo.Date (DateID);
    CREATE STATISTICS [dbo.Trip DateID stats] ON dbo.Trip (DateID);
    ```

    > [!NOTE]
    > <span data-ttu-id="3955d-261">SQL Data Warehouse no administra automáticamente las estadísticas para usted.</span><span class="sxs-lookup"><span data-stu-id="3955d-261">SQL DW does not automatically manage statistics for you.</span></span> <span data-ttu-id="3955d-262">Las estadísticas son importantes para el rendimiento de las consultas, por lo que se recomienda encarecidamente crearlas y actualizarlas.</span><span class="sxs-lookup"><span data-stu-id="3955d-262">Statistics are important for query performance and it is highly recommended you create and update statistics.</span></span>
    > 
    > <span data-ttu-id="3955d-263">**Sacará el máximo provecho con las estadísticas en columnas relacionadas con combinaciones, columnas que se usan en la cláusula WHERE y columnas de GROUP BY.**</span><span class="sxs-lookup"><span data-stu-id="3955d-263">**You gain the most benefit by having statistics on columns involved in joins, columns used in the WHERE clause and columns found in GROUP BY.**</span></span>
    >

3. <span data-ttu-id="3955d-264">Ejecute de nuevo la consulta desde los requisitos previos y observe las diferencias de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="3955d-264">Run the query from Prerequisites again and observe any performance differences.</span></span> <span data-ttu-id="3955d-265">Aunque las diferencias de rendimiento de las consultas no serán tan importantes como con el escalado vertical, notará un aumento de la velocidad.</span><span class="sxs-lookup"><span data-stu-id="3955d-265">While the differences in query performance will not be as drastic as scaling up, you should notice a  speed-up.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3955d-266">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3955d-266">Next steps</span></span>

<span data-ttu-id="3955d-267">Ahora está listo para realizar consultas y explorar.</span><span class="sxs-lookup"><span data-stu-id="3955d-267">You're now ready to query and explore.</span></span> <span data-ttu-id="3955d-268">Consulte nuestras mejores prácticas o sugerencias.</span><span class="sxs-lookup"><span data-stu-id="3955d-268">Check out our best practices or tips.</span></span>

<span data-ttu-id="3955d-269">Si ha terminado de explorar por hoy, asegúrese de pausar la instancia.</span><span class="sxs-lookup"><span data-stu-id="3955d-269">If you're done exploring for the day, make sure to pause your instance!</span></span> <span data-ttu-id="3955d-270">En un entorno de producción, puede experimentar grandes ahorros si realiza el pausado y escalado adecuados para sus necesidades empresariales.</span><span class="sxs-lookup"><span data-stu-id="3955d-270">In production, you can experience enormous savings by pausing and scaling to meet your business needs.</span></span>

![Pausar](./media/sql-data-warehouse-get-started-tutorial/pause.png)

## <a name="useful-readings"></a><span data-ttu-id="3955d-272">Lecturas útiles</span><span class="sxs-lookup"><span data-stu-id="3955d-272">Useful readings</span></span>

<span data-ttu-id="3955d-273">[Simultaneidad y administración de cargas de trabajo][]</span><span class="sxs-lookup"><span data-stu-id="3955d-273">[Concurrency and Workload Management][]</span></span>

<span data-ttu-id="3955d-274">[Procedimientos recomendados para Almacenamiento de datos SQL de Azure][]</span><span class="sxs-lookup"><span data-stu-id="3955d-274">[Best practices for Azure SQL Data Warehouse][]</span></span>

<span data-ttu-id="3955d-275">[Supervisión de consultas][]</span><span class="sxs-lookup"><span data-stu-id="3955d-275">[Query Monitoring][]</span></span>

<span data-ttu-id="3955d-276">[Top 10 Best Practices for Building a Large Scale Relational Data Warehouse][] (Los 10 mejores procedimientos para compilar un almacén de datos relacionales a gran escala)</span><span class="sxs-lookup"><span data-stu-id="3955d-276">[Top 10 Best Practices for Building a Large Scale Relational Data Warehouse][]</span></span>

<span data-ttu-id="3955d-277">[Migración de datos a Azure SQL Data Warehouse][]</span><span class="sxs-lookup"><span data-stu-id="3955d-277">[Migrating Data to Azure SQL Data Warehouse][]</span></span>

[Simultaneidad y administración de cargas de trabajo]: sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example
[Procedimientos recomendados para Almacenamiento de datos SQL de Azure]: sql-data-warehouse-best-practices.md#hash-distribute-large-tables
[Supervisión de consultas]: sql-data-warehouse-manage-monitor.md
[Top 10 Best Practices for Building a Large Scale Relational Data Warehouse]: https://blogs.msdn.microsoft.com/sqlcat/2013/09/16/top-10-best-practices-for-building-a-large-scale-relational-data-warehouse/ (Los 10 mejores procedimientos para compilar un almacén de datos relacionales a gran escala)
[Migración de datos a Azure SQL Data Warehouse]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/



[!INCLUDE [Additional Resources](../../includes/sql-data-warehouse-article-footer.md)]

<!-- Internal Links -->
[requisitos previos]: sql-data-warehouse-get-started-tutorial.md#prerequisites

<!--Other Web references-->
[Visual Studio]: https://www.visualstudio.com/
[SQL Server Management Studio]: https://msdn.microsoft.com/en-us/library/mt238290.aspx
