---
title: "Introducción aaaAzure almacenamiento de datos de SQL - tutorial | Documentos de Microsoft"
description: "Este tutorial le enseña cómo tooprovision y cargar datos en almacenamiento de datos de SQL Azure. También aprenderá los conceptos básicos de hello sobre el ajuste de escala, la pausa y la optimización."
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
ms.openlocfilehash: edd2a21b0fe49ca8e9792c7c512310339a822c55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-data-warehouse"></a><span data-ttu-id="d6d08-104">Introducción a SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d6d08-104">Get started with SQL Data Warehouse</span></span>

<span data-ttu-id="d6d08-105">Este tutorial se muestra cómo tooprovision y cargar datos en almacenamiento de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="d6d08-105">This tutorial shows how tooprovision and load data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="d6d08-106">También aprenderá los conceptos básicos de hello sobre el ajuste de escala, la pausa y la optimización.</span><span class="sxs-lookup"><span data-stu-id="d6d08-106">You’ll also learn hello basics about scaling, pausing, and tuning.</span></span> <span data-ttu-id="d6d08-107">Cuando haya terminado, podrá ser tooquery listo y explorar el almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="d6d08-107">When you’re finished, you’ll be ready tooquery and explore your data warehouse.</span></span>

<span data-ttu-id="d6d08-108">**Estimado toocomplete de tiempo:** se trata de un tutorial to-end con código de ejemplo que tarda unos 30 minutos toocomplete una vez que se cumplen los requisitos previos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6d08-108">**Estimated time toocomplete:** This is an end-to-end tutorial with example code that takes about 30 minutes toocomplete once you have met hello prerequisites.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d6d08-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d6d08-109">Prerequisites</span></span>

<span data-ttu-id="d6d08-110">tutorial de Hola se da por supuesto que está familiarizado con los conceptos básicos de almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="d6d08-110">hello tutorial assumes you are familiar with SQL Data Warehouse basic concepts.</span></span> <span data-ttu-id="d6d08-111">Si necesita una introducción, consulte [¿Qué es SQL Data Warehouse?](sql-data-warehouse-overview-what-is.md)</span><span class="sxs-lookup"><span data-stu-id="d6d08-111">If you need an introduction, see [What is SQL Data Warehouse?](sql-data-warehouse-overview-what-is.md)</span></span> 

### <a name="sign-up-for-microsoft-azure"></a><span data-ttu-id="d6d08-112">Suscribirse a Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="d6d08-112">Sign up for Microsoft Azure</span></span>
<span data-ttu-id="d6d08-113">Si ya no tiene una cuenta de Microsoft Azure, deberá toosign a una toouse este servicio.</span><span class="sxs-lookup"><span data-stu-id="d6d08-113">If you don't already have a Microsoft Azure account, you need toosign up for one toouse this service.</span></span> <span data-ttu-id="d6d08-114">Si ya tiene una cuenta, puede omitir este paso.</span><span class="sxs-lookup"><span data-stu-id="d6d08-114">If you already have an account, you may skip this step.</span></span> 

1. <span data-ttu-id="d6d08-115">Navegar por las páginas de la cuenta de toohello [https://azure.microsoft.com/account/](https://azure.microsoft.com/account/)</span><span class="sxs-lookup"><span data-stu-id="d6d08-115">Navigate toohello account pages [https://azure.microsoft.com/account/](https://azure.microsoft.com/account/)</span></span>
2. <span data-ttu-id="d6d08-116">Cree una cuenta de Azure gratis o compre una cuenta.</span><span class="sxs-lookup"><span data-stu-id="d6d08-116">Create a free Azure account, or purchase an account.</span></span>
3. <span data-ttu-id="d6d08-117">Siga las instrucciones de Hola</span><span class="sxs-lookup"><span data-stu-id="d6d08-117">Follow hello instructions</span></span>

### <a name="install-appropriate-sql-client-drivers-and-tools"></a><span data-ttu-id="d6d08-118">Instalación de las herramientas y los controladores del cliente SQL adecuados</span><span class="sxs-lookup"><span data-stu-id="d6d08-118">Install appropriate SQL client drivers and tools</span></span>

<span data-ttu-id="d6d08-119">Mayoría de las herramientas cliente SQL puede conectarse tooSQL almacenamiento de datos mediante ADO.NET, JDBC o ODBC.</span><span class="sxs-lookup"><span data-stu-id="d6d08-119">Most SQL client tools can connect tooSQL Data Warehouse by using JDBC, ODBC, or ADO.NET.</span></span> <span data-ttu-id="d6d08-120">Debido a toohello un gran número de características de T-SQL que admite el almacenamiento de datos SQL, algunas aplicaciones cliente no son totalmente compatibles con el almacenamiento de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="d6d08-120">Due toohello large number of T-SQL features that SQL Data Warehouse supports, some client applications are not fully compatible with SQL Data Warehouse.</span></span>

<span data-ttu-id="d6d08-121">Si está ejecutando un sistema operativo Windows, se recomienda usar [Visual Studio] o [SQL Server Management Studio].</span><span class="sxs-lookup"><span data-stu-id="d6d08-121">If you are running a Windows operating system, we recommend using either [Visual Studio] or [SQL Server Management Studio].</span></span>

[!INCLUDE [Create a new logical server](../../includes/sql-data-warehouse-create-logical-server.md)] 

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="d6d08-122">Creación de Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="d6d08-122">Create a SQL Data Warehouse</span></span>

<span data-ttu-id="d6d08-123">SQL Data Warehouse es un tipo especial de base de datos diseñado para el procesamiento paralelo masivo.</span><span class="sxs-lookup"><span data-stu-id="d6d08-123">A SQL Data Warehouse is a special type of database that is designed for massively parallel processing.</span></span> <span data-ttu-id="d6d08-124">base de datos de Hola se distribuye por varios nodos y procesa las consultas en paralelo.</span><span class="sxs-lookup"><span data-stu-id="d6d08-124">hello database is distributed across multiple nodes and processes queries in parallel.</span></span> <span data-ttu-id="d6d08-125">Almacenamiento de datos de SQL tiene un nodo de control que orquesta las actividades de Hola de todos los nodos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6d08-125">SQL Data Warehouse has a control node that orchestrates hello activities of all hello nodes.</span></span> <span data-ttu-id="d6d08-126">nodos de Hello usan toomanage de base de datos SQL los datos.</span><span class="sxs-lookup"><span data-stu-id="d6d08-126">hello nodes themselves use SQL Database toomanage your data.</span></span>  

> [!NOTE]
> <span data-ttu-id="d6d08-127">La creación de una instancia de Almacenamiento de datos SQL puede dar lugar a un nuevo servicio facturable.</span><span class="sxs-lookup"><span data-stu-id="d6d08-127">Creating a SQL Data Warehouse might result in a new billable service.</span></span>  <span data-ttu-id="d6d08-128">Para más información, consulte [Precios de Azure SQL Data Warehouse](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="d6d08-128">For more information, see [SQL Data Warehouse pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span></span>
>

### <a name="create-a-data-warehouse"></a><span data-ttu-id="d6d08-129">Creación del almacenamiento de datos</span><span class="sxs-lookup"><span data-stu-id="d6d08-129">Create a data warehouse</span></span>

1. <span data-ttu-id="d6d08-130">Inicio de sesión en hello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d6d08-130">Sign into hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d6d08-131">Haga clic en **Nuevo** > **Bases de datos** > **SQL Data Warehouse**.</span><span class="sxs-lookup"><span data-stu-id="d6d08-131">Click **New** > **Databases** > **SQL Data Warehouse**.</span></span>

    <span data-ttu-id="d6d08-132">![NewBlade](../../includes/media/sql-data-warehouse-create-dw/blade-click-new.png)![SelectDW](../../includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)</span><span class="sxs-lookup"><span data-stu-id="d6d08-132">![NewBlade](../../includes/media/sql-data-warehouse-create-dw/blade-click-new.png) ![SelectDW](../../includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)</span></span>

3. <span data-ttu-id="d6d08-133">Rellene los detalles de la implementación</span><span class="sxs-lookup"><span data-stu-id="d6d08-133">Fill out deployment details</span></span>

    <span data-ttu-id="d6d08-134">**Nombre de la base de datos**: elija el que desee.</span><span class="sxs-lookup"><span data-stu-id="d6d08-134">**Database Name**: Pick anything you'd like.</span></span> <span data-ttu-id="d6d08-135">Si tiene varios almacenes de datos, se recomienda que los nombres de incluyen detalles como la región de hello, entorno, por ejemplo *mydw-oesteee. UU.-1-test*.</span><span class="sxs-lookup"><span data-stu-id="d6d08-135">If you have multiple data warehouses, we recommend your names include details such as hello region, environment, for example *mydw-westus-1-test*.</span></span>

    <span data-ttu-id="d6d08-136">**Suscripción**: su suscripción a Azure</span><span class="sxs-lookup"><span data-stu-id="d6d08-136">**Subscription**: Your Azure subscription</span></span>

    <span data-ttu-id="d6d08-137">**Grupo de recursos**: cree un grupo de recursos o seleccione uno existente.</span><span class="sxs-lookup"><span data-stu-id="d6d08-137">**Resource Group**: Create a resource group or use an existing resource group.</span></span>
    > [!NOTE]
    > <span data-ttu-id="d6d08-138">Los grupos de recursos son útiles para realizar tareas de administración de recursos como el control de acceso y la implementación de plantillas.</span><span class="sxs-lookup"><span data-stu-id="d6d08-138">Resource groups are useful for resource administration such as scoping access control and templated deployment.</span></span> <span data-ttu-id="d6d08-139">Consulte más información sobre los grupos de recursos de Azure [aquí](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="d6d08-139">Read more about Azure resource groups and best practices [here](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)</span></span>

    <span data-ttu-id="d6d08-140">**Origen**: base de datos en blanco</span><span class="sxs-lookup"><span data-stu-id="d6d08-140">**Source**: Blank Database</span></span>

    <span data-ttu-id="d6d08-141">**Servidor**: servidor hello Select que creó en [requisitos previos].</span><span class="sxs-lookup"><span data-stu-id="d6d08-141">**Server**: Select hello server you created in [Prerequisites].</span></span>

    <span data-ttu-id="d6d08-142">**Intercalación**: dejar la intercalación predeterminada de hello SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="d6d08-142">**Collation**: Leave hello default collation SQL_Latin1_General_CP1_CI_AS.</span></span>

    <span data-ttu-id="d6d08-143">**Seleccione rendimiento**: se recomienda empezar por 400DWU estándar Hola.</span><span class="sxs-lookup"><span data-stu-id="d6d08-143">**Select performance**: We recommend starting with hello standard 400DWU.</span></span>

4. <span data-ttu-id="d6d08-144">Elija **Pin toodashboard** ![tooDashboard de Pin](./media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)</span><span class="sxs-lookup"><span data-stu-id="d6d08-144">Choose **Pin toodashboard** ![Pin tooDashboard](./media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)</span></span>

5. <span data-ttu-id="d6d08-145">Póngase cómodo y espere a que su toodeploy de almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="d6d08-145">Sit back and wait for your data warehouse toodeploy!</span></span> <span data-ttu-id="d6d08-146">Es normal que este proceso tootake varios minutos.</span><span class="sxs-lookup"><span data-stu-id="d6d08-146">It's normal for this process tootake several minutes.</span></span> <span data-ttu-id="d6d08-147">portal de Hello le avisa cuando el almacenamiento de datos toouse listo.</span><span class="sxs-lookup"><span data-stu-id="d6d08-147">hello portal notifies you when your data warehouse is ready toouse.</span></span> 

## <a name="connect-toosql-data-warehouse"></a><span data-ttu-id="d6d08-148">Conectar tooSQL almacenamiento de datos</span><span class="sxs-lookup"><span data-stu-id="d6d08-148">Connect tooSQL Data Warehouse</span></span>

<span data-ttu-id="d6d08-149">Este tutorial usa el almacenamiento de datos de SQL Server Management Studio (SSMS) tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="d6d08-149">This tutorial uses SQL Server Management Studio (SSMS) tooconnect toohello data warehouse.</span></span> <span data-ttu-id="d6d08-150">Se puede conectar tooSQL almacenamiento de datos a través de estos conectores compatibles: ADO.NET, JDBC, ODBC y PHP.</span><span class="sxs-lookup"><span data-stu-id="d6d08-150">You can connect tooSQL Data Warehouse through these supported connectors: ADO.NET, JDBC, ODBC, and PHP.</span></span> <span data-ttu-id="d6d08-151">Recuerde que la funcionalidad podría ser limitada para herramientas no compatibles con Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d6d08-151">Remember, functionality might be limited for tools that are not supported by Microsoft.</span></span>


### <a name="get-connection-information"></a><span data-ttu-id="d6d08-152">Obtención de información sobre la conexión</span><span class="sxs-lookup"><span data-stu-id="d6d08-152">Get connection information</span></span>

<span data-ttu-id="d6d08-153">almacenamiento de datos de tooconnect tooyour, necesita tooconnect a través de servidor SQL lógico Hola que creó en [requisitos previos].</span><span class="sxs-lookup"><span data-stu-id="d6d08-153">tooconnect tooyour data warehouse, you need tooconnect through hello logical SQL server you created in [Prerequisites].</span></span>

1. <span data-ttu-id="d6d08-154">Seleccione el almacén de datos desde el panel de Hola o búsquelo en los recursos.</span><span class="sxs-lookup"><span data-stu-id="d6d08-154">Select your data warehouse from hello dashboard or search for it in your resources.</span></span>

    ![Panel de SQL Data Warehouse](./media/sql-data-warehouse-get-started-tutorial/sql-dw-dashboard.png)

2. <span data-ttu-id="d6d08-156">Encontrar el nombre completo de Hola para servidor SQL lógico de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6d08-156">Find hello full name for hello logical SQL server.</span></span>

    ![Seleccionar nombre del servidor](./media/sql-data-warehouse-get-started-tutorial/select-server.png)

3. <span data-ttu-id="d6d08-158">Abra SSMS y utilice el objeto explorer tooconnect toothis servidor mediante las credenciales de administrador de servidor hello que creó en [requisitos previos]</span><span class="sxs-lookup"><span data-stu-id="d6d08-158">Open SSMS and use object explorer tooconnect toothis server using hello server admin credentials you created in [Prerequisites]</span></span>

    ![Conectarse con SSMS](./media/sql-data-warehouse-get-started-tutorial/ssms-connect.png)

<span data-ttu-id="d6d08-160">Si todo funciona correctamente, ahora debería tooyour conectado lógica SQL server.</span><span class="sxs-lookup"><span data-stu-id="d6d08-160">If all goes correctly, you should now be connected tooyour logical SQL server.</span></span> <span data-ttu-id="d6d08-161">Puesto que ha iniciado la sesión Hola administrador del servidor, puede conectarse tooany base de datos hospedada por servidor de hello, incluida la base de datos maestra Hola.</span><span class="sxs-lookup"><span data-stu-id="d6d08-161">Since you logged in as hello server admin, you can connect tooany database hosted by hello server, including hello master database.</span></span> 

<span data-ttu-id="d6d08-162">No hay cuenta de administrador de un solo servidor y tiene hello más privilegios de cualquier usuario.</span><span class="sxs-lookup"><span data-stu-id="d6d08-162">There is only one server admin account and it has hello most privileges of any user.</span></span> <span data-ttu-id="d6d08-163">Procure no tooallow demasiadas personas de su contraseña de administrador de organización tooknow Hola.</span><span class="sxs-lookup"><span data-stu-id="d6d08-163">Be careful not tooallow too many people in your organization tooknow hello admin password.</span></span> 

<span data-ttu-id="d6d08-164">También puede tener una cuenta de administrador de Azure Active Directory,</span><span class="sxs-lookup"><span data-stu-id="d6d08-164">You can also have an Azure active directory admin account.</span></span> <span data-ttu-id="d6d08-165">No ofrecemos detalles Hola aquí.</span><span class="sxs-lookup"><span data-stu-id="d6d08-165">We don't provide hello details here.</span></span> <span data-ttu-id="d6d08-166">Si desea que toolearn más sobre el uso de autenticación de Azure Active Directory, vea [autenticación de Azure AD](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).</span><span class="sxs-lookup"><span data-stu-id="d6d08-166">If you want toolearn more about using Azure Active Directory authentication, see [Azure AD authentication](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).</span></span>

<span data-ttu-id="d6d08-167">A continuación, veremos la creación de usuarios e inicios de sesión adicionales.</span><span class="sxs-lookup"><span data-stu-id="d6d08-167">Next, we explore creating additional logins and users.</span></span>


## <a name="create-a-database-user"></a><span data-ttu-id="d6d08-168">Creación de un usuario de base de datos</span><span class="sxs-lookup"><span data-stu-id="d6d08-168">Create a database user</span></span>

<span data-ttu-id="d6d08-169">En este paso, creará un tooaccess de cuenta de usuario a su almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="d6d08-169">In this step, you create a user account tooaccess your data warehouse.</span></span> <span data-ttu-id="d6d08-170">También le mostraremos cómo toogive ese toorun de capacidad de usuario hello las consultas con una gran cantidad de memoria y recursos de CPU.</span><span class="sxs-lookup"><span data-stu-id="d6d08-170">We also show you how toogive that user hello ability toorun queries with a large amount of memory and CPU resources.</span></span>

### <a name="notes-about-resource-classes-for-allocating-resources-tooqueries"></a><span data-ttu-id="d6d08-171">Notas acerca de las clases de recursos para la asignación de recursos tooqueries</span><span class="sxs-lookup"><span data-stu-id="d6d08-171">Notes about resource classes for allocating resources tooqueries</span></span>

- <span data-ttu-id="d6d08-172">tookeep los datos seguros, no use las consultas toorun de administración de servidor de hello en las bases de datos de producción.</span><span class="sxs-lookup"><span data-stu-id="d6d08-172">tookeep your data safe, don't use hello server admin toorun queries on your production databases.</span></span> <span data-ttu-id="d6d08-173">Tiene más privilegios de cualquier usuario hello y mediante tooperform operaciones en los datos de usuario coloca los datos en peligro.</span><span class="sxs-lookup"><span data-stu-id="d6d08-173">It has hello most privileges of any user and using it tooperform operations on user data puts your data at risk.</span></span> <span data-ttu-id="d6d08-174">Además, puesto que Hola, Administrador de servidor se ha diseñado tooperform las operaciones de administración, se ejecuta operaciones con solo una pequeña asignación de memoria y recursos de CPU.</span><span class="sxs-lookup"><span data-stu-id="d6d08-174">Also, since hello server admin is meant tooperform management operations, it runs operations with only a small allocation of memory and CPU resources.</span></span> 

- <span data-ttu-id="d6d08-175">Almacenamiento de datos de SQL utiliza las funciones de base de datos predefinidos, llamado a las clases de recursos, tooallocate distintas cantidades de memoria, los recursos de CPU y toousers de ranuras de simultaneidad.</span><span class="sxs-lookup"><span data-stu-id="d6d08-175">SQL Data Warehouse uses pre-defined database roles, called resource classes, tooallocate different amounts of memory, CPU resources, and concurrency slots toousers.</span></span> <span data-ttu-id="d6d08-176">Cada usuario puede pertenecer tooa clase de recursos pequeño, mediano, grande o extragrande.</span><span class="sxs-lookup"><span data-stu-id="d6d08-176">Each user can belong tooa small, medium, large, or extra-large resource class.</span></span> <span data-ttu-id="d6d08-177">Hello clase de recurso del usuario determina Hola recursos Hola usuario tiene toorun consultas y operaciones de carga.</span><span class="sxs-lookup"><span data-stu-id="d6d08-177">hello user's resource class determines hello resources hello user has toorun queries and load operations.</span></span>

- <span data-ttu-id="d6d08-178">Para la compresión de datos óptima, usuario Hola puede necesitar tooload con grandes o asignaciones de recursos extra grande.</span><span class="sxs-lookup"><span data-stu-id="d6d08-178">For optimal data compression, hello user may need tooload with large or extra large resource allocations.</span></span> <span data-ttu-id="d6d08-179">Obtenga más información sobre las clases de recursos [aquí](./sql-data-warehouse-develop-concurrency.md#resource-classes):</span><span class="sxs-lookup"><span data-stu-id="d6d08-179">Read more about resource classes [here](./sql-data-warehouse-develop-concurrency.md#resource-classes):</span></span>

### <a name="create-an-account-that-can-control-a-database"></a><span data-ttu-id="d6d08-180">Creación de una cuenta que puede controlar una base de datos</span><span class="sxs-lookup"><span data-stu-id="d6d08-180">Create an account that can control a database</span></span>

<span data-ttu-id="d6d08-181">Dado que han iniciado sesión en como administrador del servidor de Hola tiene usuarios e inicios de sesión de toocreate de permisos.</span><span class="sxs-lookup"><span data-stu-id="d6d08-181">Since you are currently logged in as hello server admin you have permissions toocreate logins and users.</span></span>

1. <span data-ttu-id="d6d08-182">Con SSMS u otro cliente de consulta, abra una nueva consulta para **master**.</span><span class="sxs-lookup"><span data-stu-id="d6d08-182">Using SSMS or another query client, open a new query for **master**.</span></span>

    ![Nueva consulta en Master](./media/sql-data-warehouse-get-started-tutorial/query-on-server.png)

    ![Nueva consulta en Master1](./media/sql-data-warehouse-get-started-tutorial/query-on-master.png)

2. <span data-ttu-id="d6d08-185">En la ventana de consulta de hello, ejecute este toocreate de comando de T-SQL un inicio de sesión denominado MedRCLogin y un usuario denominado LoadingUser.</span><span class="sxs-lookup"><span data-stu-id="d6d08-185">In hello query window, run this T-SQL command toocreate a login named MedRCLogin and user named LoadingUser.</span></span> <span data-ttu-id="d6d08-186">Este inicio de sesión puede conectarse toohello lógica SQL server.</span><span class="sxs-lookup"><span data-stu-id="d6d08-186">This login can connect toohello logical SQL server.</span></span>

    ```sql
    CREATE LOGIN MedRCLogin WITH PASSWORD = 'a123reallySTRONGpassword!';
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

3. <span data-ttu-id="d6d08-187">Consultar ahora Hola *base de datos de almacenamiento de datos de SQL*, cree un usuario de base de datos basado en Hola inicio de sesión creado tooaccess y realizar operaciones en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6d08-187">Now querying hello *SQL Data Warehouse database*, create a database user based on hello login you created tooaccess and perform operations on hello database.</span></span>

    ```sql
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

4. <span data-ttu-id="d6d08-188">Asigne Hola usuario control permisos toohello base de datos denominada NYT.</span><span class="sxs-lookup"><span data-stu-id="d6d08-188">Give hello database user control permissions toohello database called NYT.</span></span> 

    ```sql
    GRANT CONTROL ON DATABASE::[NYT] tooLoadingUser;
    ```
    > [!NOTE]
    > <span data-ttu-id="d6d08-189">Si el nombre de la base de datos tiene guiones en ella, puede toowrap seguro de que entre corchetes.</span><span class="sxs-lookup"><span data-stu-id="d6d08-189">If your database name has hyphens in it, be sure toowrap it in brackets!</span></span> 
    >

### <a name="give-hello-user-medium-resource-allocations"></a><span data-ttu-id="d6d08-190">Proporcionar a las asignaciones del medio de recursos de usuario de Hola</span><span class="sxs-lookup"><span data-stu-id="d6d08-190">Give hello user medium resource allocations</span></span>

1. <span data-ttu-id="d6d08-191">Ejecute este toomake de comando de T-SQL TI un miembro de clase de recurso intermedio hello, que se denomina mediumrc.</span><span class="sxs-lookup"><span data-stu-id="d6d08-191">Run this T-SQL command toomake it a member of hello medium resource class, which is called mediumrc.</span></span> 

    ```sql
    EXEC sp_addrolemember 'mediumrc', 'LoadingUser';
    ```
    > [!NOTE]
    > <span data-ttu-id="d6d08-192">Haga clic en [aquí](sql-data-warehouse-develop-concurrency.md#resource-classes) toolearn más información acerca de las clases de simultaneidad y recursos.</span><span class="sxs-lookup"><span data-stu-id="d6d08-192">Click [here](sql-data-warehouse-develop-concurrency.md#resource-classes) toolearn more about concurrency and resource classes!</span></span> 
    >

2. <span data-ttu-id="d6d08-193">Conectar el servidor lógico toohello con nuevas credenciales de Hola</span><span class="sxs-lookup"><span data-stu-id="d6d08-193">Connect toohello logical server with hello new credentials</span></span>

    ![Inicie sesión con el nuevo inicio de sesión](./media/sql-data-warehouse-get-started-tutorial/new-login.png)


## <a name="load-data-from-azure-blob-storage"></a><span data-ttu-id="d6d08-195">Carga de datos del almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="d6d08-195">Load data from Azure blob storage</span></span>

<span data-ttu-id="d6d08-196">Ahora está listo tooload datos en el almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="d6d08-196">You are now ready tooload data into your data warehouse.</span></span> <span data-ttu-id="d6d08-197">Este paso muestra cómo de blob de datos de archivo cab de tooload ciudad de Nueva York taxi desde un almacenamiento de Azure público.</span><span class="sxs-lookup"><span data-stu-id="d6d08-197">This step shows you how tooload New York City taxi cab data from a public Azure storage blob.</span></span> 

- <span data-ttu-id="d6d08-198">Una manera común de datos de tooload en almacenamiento de datos de SQL están toofirst mover el almacenamiento de blobs de hello datos tooAzure y, a continuación, cargarlos en el almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="d6d08-198">A common way tooload data into SQL Data Warehouse is toofirst move hello data tooAzure blob storage, and then load it into your data warehouse.</span></span> <span data-ttu-id="d6d08-199">toomake sea más fácil toounderstand cómo tooload, tenemos datos de archivo cab de Nueva York taxi ya hospedadas en un blob de almacenamiento de Azure pública.</span><span class="sxs-lookup"><span data-stu-id="d6d08-199">toomake it easier toounderstand how tooload, we have New York taxi cab data already hosted in a public Azure storage blob.</span></span> 

- <span data-ttu-id="d6d08-200">En el futuro, toolearn cómo tooget su tooAzure datos blob almacenamiento o tooload directamente desde el origen en almacenamiento de datos de SQL, vea hello [cargar información general sobre](sql-data-warehouse-overview-load.md).</span><span class="sxs-lookup"><span data-stu-id="d6d08-200">For future reference, toolearn how tooget your data tooAzure blob storage or tooload it directly from your source into SQL Data Warehouse, see hello [loading overview](sql-data-warehouse-overview-load.md).</span></span>


### <a name="define-external-data"></a><span data-ttu-id="d6d08-201">Definición de datos externos</span><span class="sxs-lookup"><span data-stu-id="d6d08-201">Define external data</span></span>

1. <span data-ttu-id="d6d08-202">Cree una clave maestra.</span><span class="sxs-lookup"><span data-stu-id="d6d08-202">Create a master key.</span></span> <span data-ttu-id="d6d08-203">Solo necesita toocreate una clave maestra de una vez por cada base de datos.</span><span class="sxs-lookup"><span data-stu-id="d6d08-203">You only need toocreate a master key once per database.</span></span> 

    ```sql
    CREATE MASTER KEY;
    ```

2. <span data-ttu-id="d6d08-204">Definir la ubicación de Hola de hello Azure blob que contiene los datos de archivo cab de hello taxi.</span><span class="sxs-lookup"><span data-stu-id="d6d08-204">Define hello location of hello Azure blob that contains hello taxi cab data.</span></span>  

    ```sql
    CREATE EXTERNAL DATA SOURCE NYTPublic
    WITH
    (
        TYPE = Hadoop,
        LOCATION = 'wasbs://2013@nytpublic.blob.core.windows.net/'
    );
    ```

3. <span data-ttu-id="d6d08-205">Definir los formatos de archivo externo de Hola</span><span class="sxs-lookup"><span data-stu-id="d6d08-205">Define hello external file formats</span></span>

    <span data-ttu-id="d6d08-206">Hola ```CREATE EXTERNAL FILE FORMAT``` comando es toospecify usa el formato de archivos que contienen datos externos de saludo.</span><span class="sxs-lookup"><span data-stu-id="d6d08-206">hello ```CREATE EXTERNAL FILE FORMAT``` command is used toospecify the format of files that contain hello external data.</span></span> <span data-ttu-id="d6d08-207">Dichos archivos contienen texto separado por uno o más caracteres, denominados delimitadores.</span><span class="sxs-lookup"><span data-stu-id="d6d08-207">They contain text separated by one or more characters called delimiters.</span></span> <span data-ttu-id="d6d08-208">Con fines de demostración, los datos de archivo cab de taxi de Hola se almacenan como datos sin comprimir tanto como gzip comprimido datos.</span><span class="sxs-lookup"><span data-stu-id="d6d08-208">For demonstration purposes, hello taxi cab data is stored both as uncompressed data and as gzip compressed data.</span></span>

    <span data-ttu-id="d6d08-209">Ejecutar estos comandos T-SQL toodefine dos formatos diferentes: sin comprimir y comprimido.</span><span class="sxs-lookup"><span data-stu-id="d6d08-209">Run these T-SQL commands toodefine two different formats: uncompressed and compressed.</span></span>

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

4.  <span data-ttu-id="d6d08-210">Cree un esquema para el formato de archivos externos.</span><span class="sxs-lookup"><span data-stu-id="d6d08-210">Create a schema for your external file format.</span></span> 

    ```sql
    CREATE SCHEMA ext;
    ```
5. <span data-ttu-id="d6d08-211">Crear tablas externas de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6d08-211">Create hello external tables.</span></span> <span data-ttu-id="d6d08-212">Estas tablas hacen referencia a los datos almacenados en Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="d6d08-212">These tables reference data stored in Azure blob storage.</span></span> <span data-ttu-id="d6d08-213">Ejecute hello después toocreate de comandos de T-SQL en varias tablas externas que toohello de punto de todos los blobs de Azure hemos definido previamente en el origen de datos externo.</span><span class="sxs-lookup"><span data-stu-id="d6d08-213">Run hello following T-SQL commands toocreate several external tables that all point toohello Azure blob we defined previously in our external data source.</span></span>

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

### <a name="import-hello-data-from-azure-blob-storage"></a><span data-ttu-id="d6d08-214">Importar datos de Hola desde el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="d6d08-214">Import hello data from Azure blob storage.</span></span>

<span data-ttu-id="d6d08-215">SQL Data Warehouse admite una instrucción clave denominada CREATE TABLE AS SELECT (CTAS).</span><span class="sxs-lookup"><span data-stu-id="d6d08-215">SQL Data Warehouse supports a key statement called CREATE TABLE AS SELECT (CTAS).</span></span> <span data-ttu-id="d6d08-216">Esta instrucción crea una nueva tabla en función de los resultados de Hola de una instrucción select.</span><span class="sxs-lookup"><span data-stu-id="d6d08-216">This statement creates a new table based on hello results of a select statement.</span></span> <span data-ttu-id="d6d08-217">Hola la nueva tabla tiene Hola mismos tipos de datos y columnas como resultados de Hola de hello instrucción select.</span><span class="sxs-lookup"><span data-stu-id="d6d08-217">hello new table has hello same columns and data types as hello results of hello select statement.</span></span>  <span data-ttu-id="d6d08-218">Se trata de un forma elegante que tooimport los datos desde el almacenamiento de blobs de Azure en almacenamiento de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="d6d08-218">This is an elegant way tooimport data from Azure blob storage into SQL Data Warehouse.</span></span>

1. <span data-ttu-id="d6d08-219">Ejecute este script tooimport los datos.</span><span class="sxs-lookup"><span data-stu-id="d6d08-219">Run this script tooimport your data.</span></span>

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

2. <span data-ttu-id="d6d08-220">Consulte los datos mientras se carga.</span><span class="sxs-lookup"><span data-stu-id="d6d08-220">View your data as it loads.</span></span>

   <span data-ttu-id="d6d08-221">Está cargando varios gigabytes de datos y comprimiéndolos en índices de almacén de columnas en clúster de alto rendimiento.</span><span class="sxs-lookup"><span data-stu-id="d6d08-221">You’re loading several GBs of data and compressing it into highly performant clustered columnstore indexes.</span></span> <span data-ttu-id="d6d08-222">Ejecute hello después de consulta que usa un estado de administración dinámica (DMV) de vistas tooshow Hola de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6d08-222">Run hello following query that uses a dynamic management views (DMVs) tooshow hello status of hello load.</span></span> <span data-ttu-id="d6d08-223">Después de iniciar la consulta de hello, tome un café y una pequeña mientras el almacenamiento de datos SQL hace algún trabajo pesado.</span><span class="sxs-lookup"><span data-stu-id="d6d08-223">After starting hello query, grab a coffee and a snack while SQL Data Warehouse does some heavy lifting.</span></span>
    
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

3. <span data-ttu-id="d6d08-224">Consulte todas las consultas del sistema.</span><span class="sxs-lookup"><span data-stu-id="d6d08-224">View all system queries.</span></span>

    ```sql
    SELECT * FROM sys.dm_pdw_exec_requests;
    ```

4. <span data-ttu-id="d6d08-225">Disfrute viendo cómo los datos se cargan ordenadamente en Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d6d08-225">Enjoy seeing your data nicely loaded into your Azure SQL Data Warehouse.</span></span>

    ![Consulte los datos cargados](./media/sql-data-warehouse-get-started-tutorial/see-data-loaded.png)


## <a name="improve-query-performance"></a><span data-ttu-id="d6d08-227">Mejora del rendimiento de las consultas</span><span class="sxs-lookup"><span data-stu-id="d6d08-227">Improve query performance</span></span>

<span data-ttu-id="d6d08-228">Hay varias maneras tooimprove consulta el desempeño y tooachieve Hola rendimiento de alta velocidad que es el almacén de datos SQL diseñado tooprovide.</span><span class="sxs-lookup"><span data-stu-id="d6d08-228">There are several ways tooimprove query performance and tooachieve hello high-speed performance that SQL Data Warehouse is designed tooprovide.</span></span>  

### <a name="see-hello-effect-of-scaling-on-query-performance"></a><span data-ttu-id="d6d08-229">Ver Hola efecto de escala en el rendimiento de las consultas</span><span class="sxs-lookup"><span data-stu-id="d6d08-229">See hello effect of scaling on query performance</span></span> 

<span data-ttu-id="d6d08-230">Rendimiento de las consultas tooimprove unidireccional es tooscale recursos cambiando el nivel de servicio DWU de hello para el almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="d6d08-230">One way tooimprove query performance is tooscale resources by changing hello DWU service level for your data warehouse.</span></span> <span data-ttu-id="d6d08-231">Cada nivel de servicio cuesta más que el anterior, pero se puede reducir la escala o pausar recursos en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="d6d08-231">Each service level costs more, but you can scale back or pause resources at any time.</span></span> 

<span data-ttu-id="d6d08-232">En este paso se compara el rendimiento de dos configuraciones de DWU distintas.</span><span class="sxs-lookup"><span data-stu-id="d6d08-232">In this step, you compare performance at two different DWU settings.</span></span>

<span data-ttu-id="d6d08-233">Primero, vamos a escalar el ajuste de tamaño de hello hacia abajo too100 DWU por lo que podemos obtener una idea de cómo un nodo de proceso puede realizar por sí mismo.</span><span class="sxs-lookup"><span data-stu-id="d6d08-233">First, let's scale hello sizing down too100 DWU so we can get an idea of how one compute node might perform on its own.</span></span>

1. <span data-ttu-id="d6d08-234">Vaya toohello portal y seleccione el almacenamiento de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="d6d08-234">Go toohello portal and select your SQL Data Warehouse.</span></span>

2. <span data-ttu-id="d6d08-235">Seleccionar escala en la hoja de almacenamiento de datos SQL de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6d08-235">Select scale in hello SQL Data Warehouse blade.</span></span> 

    ![Escalado de Data Warehouse desde el portal](./media/sql-data-warehouse-get-started-tutorial/scale-dw.png)

3. <span data-ttu-id="d6d08-237">Reducir el rendimiento de hello barra too100 DWU y pulse Guardar.</span><span class="sxs-lookup"><span data-stu-id="d6d08-237">Scale down hello performance bar too100 DWU and hit save.</span></span>

    ![Escalar y guardar](./media/sql-data-warehouse-get-started-tutorial/scale-and-save.png)

4. <span data-ttu-id="d6d08-239">Espere a que su toofinish de operación de escala.</span><span class="sxs-lookup"><span data-stu-id="d6d08-239">Wait for your scale operation toofinish.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d6d08-240">No se pueden ejecutar las consultas al cambiar la escala de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6d08-240">Queries cannot run while changing hello scale.</span></span> <span data-ttu-id="d6d08-241">El escalado **elimina** las consultas actualmente en ejecución.</span><span class="sxs-lookup"><span data-stu-id="d6d08-241">Scaling **kills** your currently running queries.</span></span> <span data-ttu-id="d6d08-242">Puede reiniciarlas una vez cuando finaliza la operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6d08-242">You can restart them when hello operation is finished.</span></span>
    >
    
5. <span data-ttu-id="d6d08-243">Realice una operación de examen en los datos de ida y vuelta hello, seleccionando millones entradas superior de Hola para todas las columnas de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6d08-243">Do a scan operation on hello trip data, selecting hello top million entries for all hello columns.</span></span> <span data-ttu-id="d6d08-244">Si le toomove diligente en rápidamente, sentirse tooselect libre menos filas.</span><span class="sxs-lookup"><span data-stu-id="d6d08-244">If you're eager toomove on quickly, feel free tooselect fewer rows.</span></span> <span data-ttu-id="d6d08-245">Tome nota de Hola que tarda toorun esta operación.</span><span class="sxs-lookup"><span data-stu-id="d6d08-245">Take note of hello time it takes toorun this operation.</span></span>

    ```sql
    SELECT TOP(1000000) * FROM dbo.[Trip]
    ```
6. <span data-ttu-id="d6d08-246">Escalar el almacenamiento de datos realizar copia de DWU too400.</span><span class="sxs-lookup"><span data-stu-id="d6d08-246">Scale your data warehouse back too400 DWU.</span></span> <span data-ttu-id="d6d08-247">Recuerde que cada 100 DWU consiste en Agregar otro tooyour de nodo de proceso de almacenamiento de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="d6d08-247">Remember, each 100 DWU is adding another compute node tooyour Azure SQL Data Warehouse.</span></span>

7. <span data-ttu-id="d6d08-248">¡Vuelva a ejecutar la consulta de Hola!</span><span class="sxs-lookup"><span data-stu-id="d6d08-248">Run hello query again!</span></span> <span data-ttu-id="d6d08-249">Debe observar una diferencia significativa.</span><span class="sxs-lookup"><span data-stu-id="d6d08-249">You should notice a significant difference.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="d6d08-250">Dado que consulta Hola devuelve una gran cantidad de datos, disponibilidad de ancho de banda de Hola de máquina de hello ejecute SSMS puede ser un cuello de botella de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="d6d08-250">Because hello query returns a lot of data, hello bandwidth availability of hello machine running SSMS may be a performance bottleneck.</span></span> <span data-ttu-id="d6d08-251">Como consecuencia, es posible que no pueda ver ninguna mejora del rendimiento.</span><span class="sxs-lookup"><span data-stu-id="d6d08-251">This can result in you not seeing any performance improvements!</span></span>

> [!NOTE]
> <span data-ttu-id="d6d08-252">Como SQL Data Warehouse utiliza el procesamiento paralelo masivo,</span><span class="sxs-lookup"><span data-stu-id="d6d08-252">Since SQL Data Warehouse uses massively parallel processing.</span></span> <span data-ttu-id="d6d08-253">Las consultas que examinarán o realizan las funciones analíticas en millones de filas experimentar auténtica ventaja de Hola de almacenamiento de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="d6d08-253">Queries that scan or perform analytic functions on millions of rows experience hello true power of Azure SQL Data Warehouse.</span></span>
>

### <a name="see-hello-effect-of-statistics-on-query-performance"></a><span data-ttu-id="d6d08-254">Ver el efecto de Hola de estadísticas de rendimiento de las consultas</span><span class="sxs-lookup"><span data-stu-id="d6d08-254">See hello effect of statistics on query performance</span></span>

1. <span data-ttu-id="d6d08-255">Ejecutar una consulta que une Hola tabla de fechas con tabla de ida y vuelta de Hola</span><span class="sxs-lookup"><span data-stu-id="d6d08-255">Run a query that joins hello Date table with hello Trip table</span></span>

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

    <span data-ttu-id="d6d08-256">Esta consulta tarda algún tiempo porque almacenamiento de datos de SQL tiene datos tooshuffle antes de realizar la combinación de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6d08-256">This query takes a while because SQL Data Warehouse has tooshuffle data before it can perform hello join.</span></span> <span data-ttu-id="d6d08-257">Las combinaciones no tienen datos tooshuffle si son datos toojoin diseñado en hello igual que se distribuyó.</span><span class="sxs-lookup"><span data-stu-id="d6d08-257">Joins do not have tooshuffle data if they are designed toojoin data in hello same way it is distributed.</span></span> <span data-ttu-id="d6d08-258">Esto es un asunto más complicado.</span><span class="sxs-lookup"><span data-stu-id="d6d08-258">That's a deeper subject.</span></span> 

2. <span data-ttu-id="d6d08-259">Las estadísticas marcan la diferencia.</span><span class="sxs-lookup"><span data-stu-id="d6d08-259">Statistics make a difference.</span></span> 
3. <span data-ttu-id="d6d08-260">Ejecute este estadísticas de toocreate instrucciones en columnas de combinación de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6d08-260">Run this statement toocreate statistics on hello join columns.</span></span>

    ```sql
    CREATE STATISTICS [dbo.Date DateID stats] ON dbo.Date (DateID);
    CREATE STATISTICS [dbo.Trip DateID stats] ON dbo.Trip (DateID);
    ```

    > [!NOTE]
    > <span data-ttu-id="d6d08-261">SQL Data Warehouse no administra automáticamente las estadísticas para usted.</span><span class="sxs-lookup"><span data-stu-id="d6d08-261">SQL DW does not automatically manage statistics for you.</span></span> <span data-ttu-id="d6d08-262">Las estadísticas son importantes para el rendimiento de las consultas, por lo que se recomienda encarecidamente crearlas y actualizarlas.</span><span class="sxs-lookup"><span data-stu-id="d6d08-262">Statistics are important for query performance and it is highly recommended you create and update statistics.</span></span>
    > 
    > <span data-ttu-id="d6d08-263">**Obtenga Hola máximas ventajas al cuentan con estadísticas en las columnas que intervienen en las combinaciones, las columnas utilizadas en Hola donde se encuentran cláusula y columnas en GROUP BY.**</span><span class="sxs-lookup"><span data-stu-id="d6d08-263">**You gain hello most benefit by having statistics on columns involved in joins, columns used in hello WHERE clause and columns found in GROUP BY.**</span></span>
    >

3. <span data-ttu-id="d6d08-264">Ejecute de nuevo la consulta de Hola de requisitos previos y observe las diferencias de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="d6d08-264">Run hello query from Prerequisites again and observe any performance differences.</span></span> <span data-ttu-id="d6d08-265">Mientras que las diferencias de hello en el rendimiento de las consultas no será tan importante como el escalado, debe observar un acelerar.</span><span class="sxs-lookup"><span data-stu-id="d6d08-265">While hello differences in query performance will not be as drastic as scaling up, you should notice a  speed-up.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d6d08-266">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d6d08-266">Next steps</span></span>

<span data-ttu-id="d6d08-267">Ahora está listo tooquery y explorar.</span><span class="sxs-lookup"><span data-stu-id="d6d08-267">You're now ready tooquery and explore.</span></span> <span data-ttu-id="d6d08-268">Consulte nuestras mejores prácticas o sugerencias.</span><span class="sxs-lookup"><span data-stu-id="d6d08-268">Check out our best practices or tips.</span></span>

<span data-ttu-id="d6d08-269">Si ha terminado explorar por día de hello, asegúrese de toopause seguro de la instancia.</span><span class="sxs-lookup"><span data-stu-id="d6d08-269">If you're done exploring for hello day, make sure toopause your instance!</span></span> <span data-ttu-id="d6d08-270">En producción, puede experimentar una gran ahorro haciendo pausas y ajuste de escala toomeet sus necesidades empresariales.</span><span class="sxs-lookup"><span data-stu-id="d6d08-270">In production, you can experience enormous savings by pausing and scaling toomeet your business needs.</span></span>

![Pausar](./media/sql-data-warehouse-get-started-tutorial/pause.png)

## <a name="useful-readings"></a><span data-ttu-id="d6d08-272">Lecturas útiles</span><span class="sxs-lookup"><span data-stu-id="d6d08-272">Useful readings</span></span>

<span data-ttu-id="d6d08-273">[Simultaneidad y administración de cargas de trabajo][]</span><span class="sxs-lookup"><span data-stu-id="d6d08-273">[Concurrency and Workload Management][]</span></span>

<span data-ttu-id="d6d08-274">[Procedimientos recomendados para Almacenamiento de datos SQL de Azure][]</span><span class="sxs-lookup"><span data-stu-id="d6d08-274">[Best practices for Azure SQL Data Warehouse][]</span></span>

<span data-ttu-id="d6d08-275">[Supervisión de consultas][]</span><span class="sxs-lookup"><span data-stu-id="d6d08-275">[Query Monitoring][]</span></span>

<span data-ttu-id="d6d08-276">[Top 10 Best Practices for Building a Large Scale Relational Data Warehouse][] (Los 10 mejores procedimientos para compilar un almacén de datos relacionales a gran escala)</span><span class="sxs-lookup"><span data-stu-id="d6d08-276">[Top 10 Best Practices for Building a Large Scale Relational Data Warehouse][]</span></span>

<span data-ttu-id="d6d08-277">[Migrar datos tooAzure almacenamiento de datos SQL][]</span><span class="sxs-lookup"><span data-stu-id="d6d08-277">[Migrating Data tooAzure SQL Data Warehouse][]</span></span>

[Simultaneidad y administración de cargas de trabajo]: sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example
[Procedimientos recomendados para Almacenamiento de datos SQL de Azure]: sql-data-warehouse-best-practices.md#hash-distribute-large-tables
[Supervisión de consultas]: sql-data-warehouse-manage-monitor.md
[Top 10 Best Practices for Building a Large Scale Relational Data Warehouse]: https://blogs.msdn.microsoft.com/sqlcat/2013/09/16/top-10-best-practices-for-building-a-large-scale-relational-data-warehouse/ (Los 10 mejores procedimientos para compilar un almacén de datos relacionales a gran escala)
[Migrar datos tooAzure almacenamiento de datos SQL]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/



[!INCLUDE [Additional Resources](../../includes/sql-data-warehouse-article-footer.md)]

<!-- Internal Links -->
[requisitos previos]: sql-data-warehouse-get-started-tutorial.md#prerequisites

<!--Other Web references-->
[Visual Studio]: https://www.visualstudio.com/
[SQL Server Management Studio]: https://msdn.microsoft.com/en-us/library/mt238290.aspx
