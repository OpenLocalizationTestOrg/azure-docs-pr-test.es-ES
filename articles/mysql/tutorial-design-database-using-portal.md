---
title: "Diseño de la primera base de datos de Azure Database for MySQL: Azure Portal | Microsoft Docs"
description: "En este tutorial se explica cómo crear y administrar la base de datos y el servidor de Azure Database for MySQL con Azure Portal."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/06/2017
ms.custom: mvc
ms.openlocfilehash: c7b76cacbdc4e483353f64cc4e50c974867bb5b7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a><span data-ttu-id="56de3-103">Diseño de la primera base de datos de Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="56de3-103">Design your first Azure Database for MySQL database</span></span>
<span data-ttu-id="56de3-104">Azure Database for MySQL es un servicio administrado que le permite ejecutar, administrar y escalar bases de datos de MySQL de alta disponibilidad en la nube.</span><span class="sxs-lookup"><span data-stu-id="56de3-104">Azure Database for MySQL is a managed service that enables you to run, manage, and scale highly available MySQL databases in the cloud.</span></span> <span data-ttu-id="56de3-105">Con Azure Portal puede administrar fácilmente el servidor y diseñar una base de datos.</span><span class="sxs-lookup"><span data-stu-id="56de3-105">Using the Azure portal, you can easily manage your server and design a database.</span></span>

<span data-ttu-id="56de3-106">En este tutorial usará Azure Portal para aprender a hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="56de3-106">In this tutorial, you use the Azure portal to learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="56de3-107">Creación de una instancia de Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="56de3-107">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="56de3-108">Configuración del firewall del servidor</span><span class="sxs-lookup"><span data-stu-id="56de3-108">Configure the server firewall</span></span>
> * <span data-ttu-id="56de3-109">Usar la herramienta de línea de comandos de mysql para crear una base de datos</span><span class="sxs-lookup"><span data-stu-id="56de3-109">Use mysql command-line tool to create a database</span></span>
> * <span data-ttu-id="56de3-110">Carga de datos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="56de3-110">Load sample data</span></span>
> * <span data-ttu-id="56de3-111">Datos de consulta</span><span class="sxs-lookup"><span data-stu-id="56de3-111">Query data</span></span>
> * <span data-ttu-id="56de3-112">Actualización de datos</span><span class="sxs-lookup"><span data-stu-id="56de3-112">Update data</span></span>
> * <span data-ttu-id="56de3-113">Restauración de datos</span><span class="sxs-lookup"><span data-stu-id="56de3-113">Restore data</span></span>

## <a name="sign-in-to-the-azure-portal"></a><span data-ttu-id="56de3-114">Inicie sesión en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="56de3-114">Sign in to the Azure portal</span></span>
<span data-ttu-id="56de3-115">Abra el explorador web de su preferencia y visite [Microsoft Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="56de3-115">Open your favorite web browser, and visit the [Microsoft Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="56de3-116">Introduzca sus credenciales para iniciar sesión en el portal.</span><span class="sxs-lookup"><span data-stu-id="56de3-116">Enter your credentials to sign in to the portal.</span></span> <span data-ttu-id="56de3-117">La vista predeterminada es el panel del servicio.</span><span class="sxs-lookup"><span data-stu-id="56de3-117">The default view is your service dashboard.</span></span>

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="56de3-118">Creación de un servidor de Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="56de3-118">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="56de3-119">Se crea un servidor de Azure Database for MySQL con un conjunto definido de [recursos de proceso y almacenamiento](./concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="56de3-119">An Azure Database for MySQL server is created with a defined set of [compute and storage resources](./concepts-compute-unit-and-storage.md).</span></span> <span data-ttu-id="56de3-120">El servidor se crea dentro de un [grupo de recursos de Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span><span class="sxs-lookup"><span data-stu-id="56de3-120">The server is created within an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span></span>

1. <span data-ttu-id="56de3-121">Vaya a **Bases de datos** > **Azure Database for MySQL**.</span><span class="sxs-lookup"><span data-stu-id="56de3-121">Navigate to **Databases** > **Azure Database for MySQL**.</span></span> <span data-ttu-id="56de3-122">Si no encuentra el servidor MySQL en la categoría **Bases de datos**, haga clic en **Ver todo** para mostrar todos los servicios de base de datos disponibles.</span><span class="sxs-lookup"><span data-stu-id="56de3-122">If you cannot find MySQL Server under **Databases** category, click **See all** to show all available database services.</span></span> <span data-ttu-id="56de3-123">También puede escribir **Azure Database for MySQL** en el cuadro de búsqueda para encontrar el servicio rápidamente.</span><span class="sxs-lookup"><span data-stu-id="56de3-123">You can also type **Azure Database for MySQL** in the search box to quickly find the service.</span></span>
<span data-ttu-id="56de3-124">![2-1 Vaya a MySQL](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)</span><span class="sxs-lookup"><span data-stu-id="56de3-124">![2-1 Navigate to MySQL](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)</span></span>

2. <span data-ttu-id="56de3-125">Haga clic en el icono **Azure Database for MySQL** y, después, en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="56de3-125">Click **Azure Database for MySQL** tile, and then click **Create**.</span></span>

<span data-ttu-id="56de3-126">En nuestro ejemplo, rellene el formulario de Azure Database for MySQL con la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="56de3-126">In our example, fill out the Azure Database for MySQL form with the following information:</span></span>

| <span data-ttu-id="56de3-127">**Configuración**</span><span class="sxs-lookup"><span data-stu-id="56de3-127">**Setting**</span></span> | <span data-ttu-id="56de3-128">**Valor sugerido**</span><span class="sxs-lookup"><span data-stu-id="56de3-128">**Suggested value**</span></span> | <span data-ttu-id="56de3-129">**Descripción del campo**</span><span class="sxs-lookup"><span data-stu-id="56de3-129">**Field Description**</span></span> |
|---|---|---|
| <span data-ttu-id="56de3-130">*Nombre del servidor*</span><span class="sxs-lookup"><span data-stu-id="56de3-130">*Server name*</span></span> | <span data-ttu-id="56de3-131">myserver4demo</span><span class="sxs-lookup"><span data-stu-id="56de3-131">myserver4demo</span></span>  | <span data-ttu-id="56de3-132">El nombre del servidor debe ser único globalmente.</span><span class="sxs-lookup"><span data-stu-id="56de3-132">Server name has to be globally unique.</span></span> |
| <span data-ttu-id="56de3-133">*Suscripción*</span><span class="sxs-lookup"><span data-stu-id="56de3-133">*Subscription*</span></span> | <span data-ttu-id="56de3-134">mysubscription</span><span class="sxs-lookup"><span data-stu-id="56de3-134">mysubscription</span></span> | <span data-ttu-id="56de3-135">Seleccione la suscripción en la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="56de3-135">Select your subscription from the drop-down.</span></span> |
| <span data-ttu-id="56de3-136">*Grupos de recursos*</span><span class="sxs-lookup"><span data-stu-id="56de3-136">*Resource group*</span></span> | <span data-ttu-id="56de3-137">myresourcegroup</span><span class="sxs-lookup"><span data-stu-id="56de3-137">myresourcegroup</span></span> | <span data-ttu-id="56de3-138">Cree un grupo de recursos o use uno existente.</span><span class="sxs-lookup"><span data-stu-id="56de3-138">Create a resource group or use an existing one.</span></span> |
| <span data-ttu-id="56de3-139">*Inicio de sesión del administrador del servidor*</span><span class="sxs-lookup"><span data-stu-id="56de3-139">*Server admin login*</span></span> | <span data-ttu-id="56de3-140">myadmin</span><span class="sxs-lookup"><span data-stu-id="56de3-140">myadmin</span></span> | <span data-ttu-id="56de3-141">Nombre de la cuenta de administrador de configuración.</span><span class="sxs-lookup"><span data-stu-id="56de3-141">Setup admin account name.</span></span> |
| <span data-ttu-id="56de3-142">*Password*</span><span class="sxs-lookup"><span data-stu-id="56de3-142">*Password*</span></span> |  | <span data-ttu-id="56de3-143">Configure una contraseña de la cuenta de administrador segura.</span><span class="sxs-lookup"><span data-stu-id="56de3-143">Set a strong admin account password.</span></span> |
| <span data-ttu-id="56de3-144">*Confirmar contraseña*</span><span class="sxs-lookup"><span data-stu-id="56de3-144">*Confirm password*</span></span> |  | <span data-ttu-id="56de3-145">Confirme la contraseña de la cuenta de administrador.</span><span class="sxs-lookup"><span data-stu-id="56de3-145">Confirm the admin account password.</span></span> |
| <span data-ttu-id="56de3-146">*Ubicación*</span><span class="sxs-lookup"><span data-stu-id="56de3-146">*Location*</span></span> |  | <span data-ttu-id="56de3-147">Seleccione una región disponible.</span><span class="sxs-lookup"><span data-stu-id="56de3-147">Select an available region.</span></span> |
| <span data-ttu-id="56de3-148">*Versión*</span><span class="sxs-lookup"><span data-stu-id="56de3-148">*Version*</span></span> | <span data-ttu-id="56de3-149">5.7</span><span class="sxs-lookup"><span data-stu-id="56de3-149">5.7</span></span> | <span data-ttu-id="56de3-150">Elija la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="56de3-150">Choose the latest version.</span></span> |
| <span data-ttu-id="56de3-151">*Configurar rendimiento*</span><span class="sxs-lookup"><span data-stu-id="56de3-151">*Configure performance*</span></span> | <span data-ttu-id="56de3-152">Básico, 50 unidades de proceso, 50 GB</span><span class="sxs-lookup"><span data-stu-id="56de3-152">Basic, 50 compute units, 50 GB</span></span>  | <span data-ttu-id="56de3-153">Seleccione **Plan de tarifa**, **Unidades de proceso**, **Almacenamiento (GB)** y, finalmente, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="56de3-153">Choose **Pricing tier**, **Compute Units**, **Storage (GB)**, and then click **OK**.</span></span> |
| <span data-ttu-id="56de3-154">*Anclar al panel*</span><span class="sxs-lookup"><span data-stu-id="56de3-154">*Pin to Dashboard*</span></span> | <span data-ttu-id="56de3-155">Comprobar</span><span class="sxs-lookup"><span data-stu-id="56de3-155">Check</span></span> | <span data-ttu-id="56de3-156">Es recomendable activar esta casilla para poder encontrar el servidor fácilmente más tarde</span><span class="sxs-lookup"><span data-stu-id="56de3-156">Recommended to check this box so you may find the server easily later on</span></span> |
<span data-ttu-id="56de3-157">A continuación, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="56de3-157">Then, click **Create**.</span></span> <span data-ttu-id="56de3-158">En un par de minutos, tendrá un servidor nuevo de Azure Database for MySQL en ejecución en la nube.</span><span class="sxs-lookup"><span data-stu-id="56de3-158">In a minute or two, a new Azure Database for MySQL server is running in the cloud.</span></span> <span data-ttu-id="56de3-159">Puede hacer clic en el botón **Notificaciones** de la barra de herramientas para supervisar el proceso de implementación.</span><span class="sxs-lookup"><span data-stu-id="56de3-159">You can click **Notifications** button on the toolbar to monitor the deployment process.</span></span>

## <a name="configure-firewall"></a><span data-ttu-id="56de3-160">Configuración del firewall</span><span class="sxs-lookup"><span data-stu-id="56de3-160">Configure firewall</span></span>
<span data-ttu-id="56de3-161">Las bases de datos de Azure para MySQL están protegidas con un firewall.</span><span class="sxs-lookup"><span data-stu-id="56de3-161">Azure Databases for MySQL are protected by a firewall.</span></span> <span data-ttu-id="56de3-162">De forma predeterminada, se rechazan todas las conexiones al servidor y a las bases de datos del servidor.</span><span class="sxs-lookup"><span data-stu-id="56de3-162">By default, all connections to the server and the databases inside the server are rejected.</span></span> <span data-ttu-id="56de3-163">Antes de conectarse a Azure Database for MySQL por primera vez, configure el firewall para agregar la dirección IP (o intervalo de direcciones IP) de red pública del equipo cliente.</span><span class="sxs-lookup"><span data-stu-id="56de3-163">Before connecting to Azure Database for MySQL for the first time, configure the firewall to add the client machine's public network IP address (or IP address range).</span></span>

1. <span data-ttu-id="56de3-164">Haga clic en el servidor recién creado y, luego, en **Seguridad de la conexión**.</span><span class="sxs-lookup"><span data-stu-id="56de3-164">Click your newly created server, and then click **Connection security**.</span></span>
   <span data-ttu-id="56de3-165">![3-1 Seguridad de conexión](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)</span><span class="sxs-lookup"><span data-stu-id="56de3-165">![3-1 Connection security](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)</span></span>
2. <span data-ttu-id="56de3-166">Puede **agregar su dirección IP** o configurar aquí las reglas de firewall.</span><span class="sxs-lookup"><span data-stu-id="56de3-166">You can **Add My IP**, or configure firewall rules here.</span></span> <span data-ttu-id="56de3-167">Recuerde hacer clic en **Guardar** después de haber creado las reglas.</span><span class="sxs-lookup"><span data-stu-id="56de3-167">Remember to click **Save** after you have created the rules.</span></span>
<span data-ttu-id="56de3-168">Ahora puede conectarse al servidor con la herramienta de línea de comandos de MySQL o la herramienta MySQL Workbench de la GUI.</span><span class="sxs-lookup"><span data-stu-id="56de3-168">You can now connect to the server using mysql command-line tool or MySQL Workbench GUI tool.</span></span>

> [!TIP]
> <span data-ttu-id="56de3-169">El servidor de Azure Database for MySQL se comunica a través del puerto 3306.</span><span class="sxs-lookup"><span data-stu-id="56de3-169">Azure Database for MySQL server communicates over port 3306.</span></span> <span data-ttu-id="56de3-170">Si intenta conectarse desde una red corporativa, es posible que el firewall de la red no permita el tráfico saliente a través del puerto 3306.</span><span class="sxs-lookup"><span data-stu-id="56de3-170">If you are trying to connect from within a corporate network, outbound traffic over port 3306 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="56de3-171">En ese caso, no puede conectarse al servidor de Azure MySQL, a menos que el departamento de TI abra el puerto 3306.</span><span class="sxs-lookup"><span data-stu-id="56de3-171">If so, you cannot connect to Azure MySQL server unless your IT department opens port 3306.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="56de3-172">Obtención de información sobre la conexión</span><span class="sxs-lookup"><span data-stu-id="56de3-172">Get connection information</span></span>
<span data-ttu-id="56de3-173">Obtenga en Azure Portal el **nombre de servidor** y el **nombre de inicio de sesión de administrador de servidor** completos para el servidor de Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="56de3-173">Get the fully qualified **Server name** and **Server admin login name** for your Azure Database for MySQL server from the Azure portal.</span></span> <span data-ttu-id="56de3-174">Usará el nombre completo del servidor para conectarse al servidor a través de la herramienta de línea de comandos de MySQL.</span><span class="sxs-lookup"><span data-stu-id="56de3-174">You use the fully qualified server name to connect to your server using mysql command-line tool.</span></span> 

1. <span data-ttu-id="56de3-175">En [Azure Portal](https://portal.azure.com/), haga clic en **Todos los recursos** en el menú izquierdo, escriba el nombre y busque el servidor de Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="56de3-175">In [Azure portal](https://portal.azure.com/), click **All resources** from the left-hand menu, type the name, and search for your Azure Database for MySQL server.</span></span> <span data-ttu-id="56de3-176">Seleccione el nombre del servidor para ver los detalles.</span><span class="sxs-lookup"><span data-stu-id="56de3-176">Select the server name to view the details.</span></span>

2. <span data-ttu-id="56de3-177">En el encabezado Configuración, haga clic en **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="56de3-177">Under the Settings heading, click **Properties**.</span></span> <span data-ttu-id="56de3-178">Anote los valores de **NOMBRE DEL SERVIDOR** y **NOMBRE DE INICIO DE SESIÓN DEL ADMINISTRADOR DEL SERVIDOR**.</span><span class="sxs-lookup"><span data-stu-id="56de3-178">Note down **SERVER NAME** and **SERVER ADMIN LOGIN NAME**.</span></span> <span data-ttu-id="56de3-179">Puede hacer clic en el botón Copiar situado junto a cada campo para copiar el valor en el Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="56de3-179">You may click the copy button next to each field to copy to the clipboard.</span></span>
   <span data-ttu-id="56de3-180">![4-2 Propiedades del servidor](./media/tutorial-design-database-using-portal/4_2-server-properties.png)</span><span class="sxs-lookup"><span data-stu-id="56de3-180">![4-2 server properties](./media/tutorial-design-database-using-portal/4_2-server-properties.png)</span></span>

<span data-ttu-id="56de3-181">En este ejemplo, el nombre del servidor es *myserver4demo.mysql.database.azure.com* y el inicio de sesión del administrador del servidor, *myadmin@myserver4demo*.</span><span class="sxs-lookup"><span data-stu-id="56de3-181">In this example, the server name is *myserver4demo.mysql.database.azure.com*, and the server admin login is *myadmin@myserver4demo*.</span></span>

## <a name="connect-to-the-server-using-mysql"></a><span data-ttu-id="56de3-182">Conexión al servidor con MySQL</span><span class="sxs-lookup"><span data-stu-id="56de3-182">Connect to the server using mysql</span></span>
<span data-ttu-id="56de3-183">Use la [herramienta de línea de comandos mysql](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) para establecer una conexión con el servidor de Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="56de3-183">Use [mysql command-line tool](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) to establish a connection to your Azure Database for MySQL server.</span></span> <span data-ttu-id="56de3-184">Puede ejecutar la herramienta mysql de la línea de comandos desde Azure Cloud Shell en el explorador o desde su propio equipo mediante herramientas mysql instaladas de forma local.</span><span class="sxs-lookup"><span data-stu-id="56de3-184">You can run the mysql command-line tool from the Azure Cloud Shell in the browser or from your own machine using mysql tools installed locally.</span></span> <span data-ttu-id="56de3-185">Para iniciar Azure Cloud Shell, haga clic en el botón `Try It` situado en un bloque de código de este artículo, o visite Azure Portal y haga clic en el icono `>_` de la barra de herramientas situada en la parte superior derecha.</span><span class="sxs-lookup"><span data-stu-id="56de3-185">To launch the Azure Cloud Shell, click the `Try It` button on a code block in this article, or visit the Azure portal and click the `>_` icon in the top right toolbar.</span></span> 

<span data-ttu-id="56de3-186">Escriba el comando para conectarse:</span><span class="sxs-lookup"><span data-stu-id="56de3-186">Type the command to connect:</span></span>
```azurecli-interactive
mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

## <a name="create-a-blank-database"></a><span data-ttu-id="56de3-187">Crear una base de datos en blanco</span><span class="sxs-lookup"><span data-stu-id="56de3-187">Create a blank database</span></span>
<span data-ttu-id="56de3-188">Una vez conectado al servidor, cree una base de datos vacía con la cual trabajar.</span><span class="sxs-lookup"><span data-stu-id="56de3-188">Once you’re connected to the server, create a blank database to work with.</span></span>
```sql
CREATE DATABASE mysampledb;
```

<span data-ttu-id="56de3-189">En el símbolo del sistema, ejecute el comando siguiente para cambiar la conexión a esta base de datos recién creada:</span><span class="sxs-lookup"><span data-stu-id="56de3-189">At the prompt, run the following command to switch connection to this newly created database:</span></span>
```sql
USE mysampledb;
```

## <a name="create-tables-in-the-database"></a><span data-ttu-id="56de3-190">Creación de tablas en la base de datos</span><span class="sxs-lookup"><span data-stu-id="56de3-190">Create tables in the database</span></span>
<span data-ttu-id="56de3-191">Ahora que sabe cómo conectarse a la base de datos de Azure Database for MySQL, podemos ver cómo completar algunas tareas básicas.</span><span class="sxs-lookup"><span data-stu-id="56de3-191">Now that you know how to connect to the Azure Database for MySQL database, we can go over how to complete some basic tasks.</span></span>

<span data-ttu-id="56de3-192">En primer lugar, podemos crear una tabla y cargarla con algunos datos.</span><span class="sxs-lookup"><span data-stu-id="56de3-192">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="56de3-193">Vamos a crear una tabla que almacena la información del inventario.</span><span class="sxs-lookup"><span data-stu-id="56de3-193">Let's create a table that stores inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-the-tables"></a><span data-ttu-id="56de3-194">Carga de datos en las tablas</span><span class="sxs-lookup"><span data-stu-id="56de3-194">Load data into the tables</span></span>
<span data-ttu-id="56de3-195">Ahora que tenemos una tabla, podemos insertar algunos datos en ella.</span><span class="sxs-lookup"><span data-stu-id="56de3-195">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="56de3-196">En la ventana de símbolo del sistema abierta, ejecute la consulta siguiente para insertar algunas filas de datos.</span><span class="sxs-lookup"><span data-stu-id="56de3-196">At the open command prompt window, run the following query to insert some rows of data.</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="56de3-197">Ahora tiene dos filas de datos de ejemplo en la tabla que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="56de3-197">Now you have two rows of sample data into the table you created earlier.</span></span>

## <a name="query-and-update-the-data-in-the-tables"></a><span data-ttu-id="56de3-198">Consulta y actualización de los datos en las tablas</span><span class="sxs-lookup"><span data-stu-id="56de3-198">Query and update the data in the tables</span></span>
<span data-ttu-id="56de3-199">Ejecute la consulta siguiente para recuperar información de la tabla de base de datos.</span><span class="sxs-lookup"><span data-stu-id="56de3-199">Execute the following query to retrieve information from the database table.</span></span>
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="56de3-200">También puede actualizar los datos en las tablas.</span><span class="sxs-lookup"><span data-stu-id="56de3-200">You can also update the data in the tables.</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="56de3-201">La fila se actualiza en consecuencia cuando se recuperan los datos.</span><span class="sxs-lookup"><span data-stu-id="56de3-201">The row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-to-a-previous-point-in-time"></a><span data-ttu-id="56de3-202">Restauración de una base de datos a un momento anterior en el tiempo</span><span class="sxs-lookup"><span data-stu-id="56de3-202">Restore a database to a previous point in time</span></span>
<span data-ttu-id="56de3-203">Imagine que ha eliminado accidentalmente una tabla de base de datos importantes y no puede recuperar los datos fácilmente.</span><span class="sxs-lookup"><span data-stu-id="56de3-203">Imagine you have accidentally deleted an important database table, and cannot recover the data easily.</span></span> <span data-ttu-id="56de3-204">Azure Database for MySQL permite restaurar el servidor a un momento dado, ya que crea una copia de las bases de datos en un nuevo servidor.</span><span class="sxs-lookup"><span data-stu-id="56de3-204">Azure Database for MySQL allows you to restore the server to a point in time, creating a copy of the databases into new server.</span></span> <span data-ttu-id="56de3-205">Puede usar este servidor nuevo para recuperar los datos eliminados.</span><span class="sxs-lookup"><span data-stu-id="56de3-205">You can use this new server to recover your deleted data.</span></span> <span data-ttu-id="56de3-206">Los pasos siguientes restauran el servidor de ejemplo a un punto antes de que se agregara la tabla.</span><span class="sxs-lookup"><span data-stu-id="56de3-206">The following steps restore the sample server to a point before the table was added.</span></span>

1. <span data-ttu-id="56de3-207">En Azure Portal, localice Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="56de3-207">In the Azure portal, locate your Azure Database for MySQL.</span></span> <span data-ttu-id="56de3-208">En la página **Información general**, haga clic en **Restaurar** en la barra de herramientas.</span><span class="sxs-lookup"><span data-stu-id="56de3-208">On the **Overview** page, click **Restore** on the toolbar.</span></span> <span data-ttu-id="56de3-209">Se abre la página de restauración.</span><span class="sxs-lookup"><span data-stu-id="56de3-209">The Restore page opens.</span></span>

   ![10-1 Restaurar una base de datos](./media/tutorial-design-database-using-portal/10_1-restore-a-db.png)

2. <span data-ttu-id="56de3-211">Rellene el formulario de **restauración** con la información necesaria.</span><span class="sxs-lookup"><span data-stu-id="56de3-211">Fill out the **Restore** form with the required information.</span></span>
   
   ![10-2 Formulario de restauración](./media/tutorial-design-database-using-portal/10_2-restore-form.png)
   
   - <span data-ttu-id="56de3-213">**Punto de restauración**: seleccione un momento dado al que quiere restaurar, en el período de tiempo que aparece.</span><span class="sxs-lookup"><span data-stu-id="56de3-213">**Restore point**: Select a point-in-time that you want to restore to, within the timeframe listed.</span></span> <span data-ttu-id="56de3-214">Asegúrese de que convierte la zona horaria local a UTC.</span><span class="sxs-lookup"><span data-stu-id="56de3-214">Make sure to convert your local timezone to UTC.</span></span>
   - <span data-ttu-id="56de3-215">**Restaurar en el servidor nuevo**: especifique el nombre del nuevo servidor donde quiere restaurar.</span><span class="sxs-lookup"><span data-stu-id="56de3-215">**Restore to new server**: Provide a new server name you want to restore to.</span></span>
   - <span data-ttu-id="56de3-216">**Ubicación**: la región es la misma que la del servidor de origen y no se puede cambiar.</span><span class="sxs-lookup"><span data-stu-id="56de3-216">**Location**: The region is same as the source server, and cannot be changed.</span></span>
   - <span data-ttu-id="56de3-217">**Plan de tarifa**: es el mismo que el del servidor de origen y no se puede cambiar.</span><span class="sxs-lookup"><span data-stu-id="56de3-217">**Pricing tier**: The pricing tier is the same as the source server, and cannot be changed.</span></span>
   
3. <span data-ttu-id="56de3-218">Haga clic en **Aceptar** para restaurar el servidor a un [momento dado](./howto-restore-server-portal.md) antes de que se eliminara la tabla.</span><span class="sxs-lookup"><span data-stu-id="56de3-218">Click **OK** to restore the server to [restore to a point in time](./howto-restore-server-portal.md) before the table was deleted.</span></span> <span data-ttu-id="56de3-219">Al restaurar un servidor, se crea una nueva copia del servidor a partir del momento dado que especifique.</span><span class="sxs-lookup"><span data-stu-id="56de3-219">Restoring a server creates a new copy of the server, as of the point in time you specify.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="56de3-220">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="56de3-220">Next steps</span></span>
<span data-ttu-id="56de3-221">En este tutorial uso Azure Portal para aprender a hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="56de3-221">In this tutorial, you use the Azure portal to learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="56de3-222">Creación de una instancia de Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="56de3-222">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="56de3-223">Configuración del firewall del servidor</span><span class="sxs-lookup"><span data-stu-id="56de3-223">Configure the server firewall</span></span>
> * <span data-ttu-id="56de3-224">Usar la herramienta de línea de comandos de mysql para crear una base de datos</span><span class="sxs-lookup"><span data-stu-id="56de3-224">Use mysql command-line tool to create a database</span></span>
> * <span data-ttu-id="56de3-225">Carga de datos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="56de3-225">Load sample data</span></span>
> * <span data-ttu-id="56de3-226">Datos de consulta</span><span class="sxs-lookup"><span data-stu-id="56de3-226">Query data</span></span>
> * <span data-ttu-id="56de3-227">Actualización de datos</span><span class="sxs-lookup"><span data-stu-id="56de3-227">Update data</span></span>
> * <span data-ttu-id="56de3-228">Restauración de datos</span><span class="sxs-lookup"><span data-stu-id="56de3-228">Restore data</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="56de3-229">Conexión de aplicaciones a Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="56de3-229">How to connect applications to Azure Database for MySQL</span></span>](./howto-connection-string.md)
