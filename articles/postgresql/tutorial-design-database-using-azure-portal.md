---
title: "Diseño de la primera base de datos de Azure Database for PostgreSQL con Azure Portal | Microsoft Docs"
description: "En este tutorial se muestra cómo diseñar la primera base de datos de Azure Database for PostgreSQL con Azure Portal."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: tutorial, mvc
ms.topic: tutorial
ms.date: 05/10/2017
ms.openlocfilehash: 2aa9d10749b54537495ad3e09566c43718f67a9e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="design-your-first-azure-database-for-postgresql-using-the-azure-portal"></a><span data-ttu-id="9121a-103">Diseño de la primera base de datos de Azure Database for PostgreSQL con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9121a-103">Design your first Azure Database for PostgreSQL using the Azure portal</span></span>

<span data-ttu-id="9121a-104">Azure Database for PostgreSQL es un servicio administrado que le permite ejecutar, administrar y escalar bases de datos de PostgreSQL de alta disponibilidad en la nube.</span><span class="sxs-lookup"><span data-stu-id="9121a-104">Azure Database for PostgreSQL is a managed service that enables you to run, manage, and scale highly available PostgreSQL databases in the cloud.</span></span> <span data-ttu-id="9121a-105">Con Azure Portal puede administrar fácilmente el servidor y diseñar una base de datos.</span><span class="sxs-lookup"><span data-stu-id="9121a-105">Using the Azure portal, you can easily manage your server and design a database.</span></span>

<span data-ttu-id="9121a-106">En este tutorial usará Azure Portal para aprender a hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="9121a-106">In this tutorial, you use the Azure portal to learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="9121a-107">Creación de una base de datos de Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="9121a-107">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="9121a-108">Configuración del firewall del servidor</span><span class="sxs-lookup"><span data-stu-id="9121a-108">Configure the server firewall</span></span>
> * <span data-ttu-id="9121a-109">Uso de la utilidad [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) para crear una base de datos</span><span class="sxs-lookup"><span data-stu-id="9121a-109">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility to create a database</span></span>
> * <span data-ttu-id="9121a-110">Carga de datos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="9121a-110">Load sample data</span></span>
> * <span data-ttu-id="9121a-111">Datos de consulta</span><span class="sxs-lookup"><span data-stu-id="9121a-111">Query data</span></span>
> * <span data-ttu-id="9121a-112">Actualización de datos</span><span class="sxs-lookup"><span data-stu-id="9121a-112">Update data</span></span>
> * <span data-ttu-id="9121a-113">Restauración de datos</span><span class="sxs-lookup"><span data-stu-id="9121a-113">Restore data</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9121a-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9121a-114">Prerequisites</span></span>
<span data-ttu-id="9121a-115">Si no tiene una suscripción a Azure, cree una cuenta [gratuita](https://azure.microsoft.com/free/) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="9121a-115">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="9121a-116">Iniciar sesión en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9121a-116">Log in to the Azure portal</span></span>
<span data-ttu-id="9121a-117">Inicie sesión en [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9121a-117">Log in to the [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-an-azure-database-for-postgresql"></a><span data-ttu-id="9121a-118">Creación de una instancia de Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="9121a-118">Create an Azure Database for PostgreSQL</span></span>

<span data-ttu-id="9121a-119">Un servidor de Azure Database for PostgreSQL se crea con un conjunto definido de [recursos de proceso y almacenamiento](./concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="9121a-119">An Azure Database for PostgreSQL server is created with a defined set of [compute and storage resources](./concepts-compute-unit-and-storage.md).</span></span> <span data-ttu-id="9121a-120">El servidor se crea dentro de un [grupo de recursos de Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9121a-120">The server is created within an [Azure resource group](../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="9121a-121">Para crear un servidor de Azure Database for PostgreSQL, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="9121a-121">Follow these steps to create an Azure Database for PostgreSQL server:</span></span>
1.  <span data-ttu-id="9121a-122">Haga clic en el botón **+ Nuevo** de la esquina superior izquierda de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="9121a-122">Click the **+ New**  button found on the upper left-hand corner of the Azure portal.</span></span>
2.  <span data-ttu-id="9121a-123">En la página **Nuevo**, seleccione **Bases de datos** y, en la página **Bases de datos**, seleccione **Azure Database for PostgreSQL**.</span><span class="sxs-lookup"><span data-stu-id="9121a-123">Select **Databases** from the **New** page, and select **Azure Database for PostgreSQL** from the **Databases** page.</span></span>
 <span data-ttu-id="9121a-124">![Azure Database for PostgreSQL: creación de la base de datos](./media/tutorial-design-database-using-azure-portal/1-create-database.png)</span><span class="sxs-lookup"><span data-stu-id="9121a-124">![Azure Database for PostgreSQL - Create the database](./media/tutorial-design-database-using-azure-portal/1-create-database.png)</span></span>

3.  <span data-ttu-id="9121a-125">Rellene el formulario con los datos del nuevo servidor con la siguiente información, como se muestra en la imagen anterior:</span><span class="sxs-lookup"><span data-stu-id="9121a-125">Fill out the new server details form with the following information, as shown on the preceding image:</span></span>
    - <span data-ttu-id="9121a-126">Nombre del servidor: **mypgserver-20170401** (el nombre del servidor se asigna al nombre DNS y, por tanto, debe ser único a nivel global)</span><span class="sxs-lookup"><span data-stu-id="9121a-126">Server name: **mypgserver-20170401** (name of a server maps to DNS name and is thus required to be globally unique)</span></span> 
    - <span data-ttu-id="9121a-127">Suscripción: si tiene varias, elija la suscripción donde se encuentre el recurso o para la cual se facture.</span><span class="sxs-lookup"><span data-stu-id="9121a-127">Subscription: If you have multiple subscriptions, choose the appropriate subscription in which the resource exists or is billed for.</span></span>
    - <span data-ttu-id="9121a-128">Grupo de recursos: **myresourcegroup**</span><span class="sxs-lookup"><span data-stu-id="9121a-128">Resource group: **myresourcegroup**</span></span>
    - <span data-ttu-id="9121a-129">El inicio de sesión de administrador y la contraseña que elija para el servidor</span><span class="sxs-lookup"><span data-stu-id="9121a-129">Server admin login and password of your choice</span></span>
    - <span data-ttu-id="9121a-130">Ubicación</span><span class="sxs-lookup"><span data-stu-id="9121a-130">Location</span></span>
    - <span data-ttu-id="9121a-131">Versión de PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="9121a-131">PostgreSQL Version</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="9121a-132">Se requiere el inicio de sesión y la contraseña de administrador de servidor que especifique aquí para iniciar sesión en el servidor y a sus bases de datos más adelante en esta guía de inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="9121a-132">The server admin login and password that you specify here are required to log in to the server and its databases later in this quick start.</span></span> <span data-ttu-id="9121a-133">Recuerde o grabe esta información para su uso posterior.</span><span class="sxs-lookup"><span data-stu-id="9121a-133">Remember or record this information for later use.</span></span>

4.  <span data-ttu-id="9121a-134">Haga clic en **Plan de tarifa** para especificar el tanto el nivel de rendimiento como el nivel de servicio de la nueva base de datos.</span><span class="sxs-lookup"><span data-stu-id="9121a-134">Click **Pricing tier** to specify the service tier and performance level for your new database.</span></span> <span data-ttu-id="9121a-135">En esta guía de inicio rápido, seleccione el nivel **Básico**, **50 Unidades de proceso** y **50 GB** de almacenamiento incluido.</span><span class="sxs-lookup"><span data-stu-id="9121a-135">For this quick start, select **Basic** Tier, **50 Compute Units** and **50 GB** of included storage.</span></span>
 <span data-ttu-id="9121a-136">![Azure Database for PostgreSQL: selección del nivel de servicio](./media/tutorial-design-database-using-azure-portal/2-service-tier.png)</span><span class="sxs-lookup"><span data-stu-id="9121a-136">![Azure Database for PostgreSQL - pick the service tier](./media/tutorial-design-database-using-azure-portal/2-service-tier.png)</span></span>
5.  <span data-ttu-id="9121a-137">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="9121a-137">Click **Ok**.</span></span>
6.  <span data-ttu-id="9121a-138">Haga clic en **Crear** para realizar el aprovisionamiento del servidor.</span><span class="sxs-lookup"><span data-stu-id="9121a-138">Click **Create** to provision the server.</span></span> <span data-ttu-id="9121a-139">El aprovisionamiento tarda unos minutos.</span><span class="sxs-lookup"><span data-stu-id="9121a-139">Provisioning takes a few minutes.</span></span>

  > [!TIP]
  > <span data-ttu-id="9121a-140">Marque la opción **Anclar al panel** para realizar el seguimiento de las implementaciones fácilmente.</span><span class="sxs-lookup"><span data-stu-id="9121a-140">Check the **Pin to dashboard** option to allow easy tracking of your deployments.</span></span>

7.  <span data-ttu-id="9121a-141">En la barra de herramientas, haga clic en **Notificaciones** para supervisar el proceso de implementación.</span><span class="sxs-lookup"><span data-stu-id="9121a-141">On the toolbar, click **Notifications** to monitor the deployment process.</span></span>
 <span data-ttu-id="9121a-142">![Azure Database for PostgreSQL: consulta de las notificaciones](./media/tutorial-design-database-using-azure-portal/3-notifications.png)</span><span class="sxs-lookup"><span data-stu-id="9121a-142">![Azure Database for PostgreSQL - See notifications](./media/tutorial-design-database-using-azure-portal/3-notifications.png)</span></span>
   
  <span data-ttu-id="9121a-143">De forma predeterminada, la base de datos de **postgres** se crea en el servidor.</span><span class="sxs-lookup"><span data-stu-id="9121a-143">By default, **postgres** database gets created under your server.</span></span> <span data-ttu-id="9121a-144">La base de datos [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) es una base de datos predeterminada pensada para que la usen los usuarios, las utilidades y aplicaciones de otros fabricantes.</span><span class="sxs-lookup"><span data-stu-id="9121a-144">The [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is a default database meant for use by users, utilities, and third-party applications.</span></span> 

## <a name="configure-a-server-level-firewall-rule"></a><span data-ttu-id="9121a-145">Configuración de una regla de firewall de nivel de servidor</span><span class="sxs-lookup"><span data-stu-id="9121a-145">Configure a server-level firewall rule</span></span>

<span data-ttu-id="9121a-146">El servicio Azure Database for PostgreSQL crea un firewall en el nivel de servidor.</span><span class="sxs-lookup"><span data-stu-id="9121a-146">The Azure Database for PostgreSQL service creates a firewall at the server-level.</span></span> <span data-ttu-id="9121a-147">Este firewall evita que herramientas y aplicaciones externas se conecten al servidor o a las bases de datos de este, a menos que se cree una regla de firewall para abrirlo para direcciones IP concretas.</span><span class="sxs-lookup"><span data-stu-id="9121a-147">This firewall prevents external applications and tools from connecting to the server and any databases on the server unless a firewall rule is created to open the firewall for specific IP addresses.</span></span> 

1.  <span data-ttu-id="9121a-148">Una vez finalizada la implementación, haga clic en **Todos los recursos** del menú izquierdo y escriba el nombre **mypgserver-20170401** para buscar el servidor recién creado.</span><span class="sxs-lookup"><span data-stu-id="9121a-148">After the deployment completes, click **All Resources** from the left-hand menu and type in the name **mypgserver-20170401** to search for your newly created server.</span></span> <span data-ttu-id="9121a-149">Haga clic en el nombre del servidor que aparece en el resultado de la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="9121a-149">Click the server name listed in the search result.</span></span> <span data-ttu-id="9121a-150">Se abrirá la página **Introducción** del servidor, que proporciona opciones para continuar la configuración.</span><span class="sxs-lookup"><span data-stu-id="9121a-150">The **Overview** page for your server opens and provides options for further configuration.</span></span>
 
 ![<span data-ttu-id="9121a-151">Azure Database for PostgreSQL: búsqueda de un servidor</span><span class="sxs-lookup"><span data-stu-id="9121a-151">Azure Database for PostgreSQL - Search for server</span></span> ](./media/tutorial-design-database-using-azure-portal/4-locate.png)

2.  <span data-ttu-id="9121a-152">En la hoja del servidor, seleccione **Seguridad de la conexión**.</span><span class="sxs-lookup"><span data-stu-id="9121a-152">In the server blade, select **Connection Security**.</span></span> 
3.  <span data-ttu-id="9121a-153">Haga clic en el cuadro de texto de **Nombre de la regla,** y agregue una nueva regla de firewall para añadir el intervalo de IP de conectividad a la lista de permitidos.</span><span class="sxs-lookup"><span data-stu-id="9121a-153">Click in the text box under **Rule Name,** and add a new firewall rule to whitelist the IP range for connectivity.</span></span> <span data-ttu-id="9121a-154">Para este tutorial, vamos a permitir todas las direcciones IP; para ello, escriba **Nombre de la regla = AllowAllIps**, **IP inicial = 0.0.0.0** e **IP final = 255.255.255.255** y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="9121a-154">For this tutorial, let's allow all IPs by typing in **Rule Name = AllowAllIps**, **Start IP = 0.0.0.0** and **End IP = 255.255.255.255** and then click **Save**.</span></span> <span data-ttu-id="9121a-155">Puede establecer una regla de firewall que abarque un intervalo de IP para poder conectarse desde la red.</span><span class="sxs-lookup"><span data-stu-id="9121a-155">You can set a firewall rule that covers an IP range to be able to connect from your network.</span></span>
 
 ![Azure Database for PostgreSQL: creación de una regla de firewall](./media/tutorial-design-database-using-azure-portal/5-firewall-2.png)

4.  <span data-ttu-id="9121a-157">Haga clic en **Guardar** y en la **X** para cerrar la página **Seguridad de la conexión**.</span><span class="sxs-lookup"><span data-stu-id="9121a-157">Click **Save** and then click the **X** to close the **Connections Security** page.</span></span>

  > [!NOTE]
  > <span data-ttu-id="9121a-158">El servidor Azure PostgreSQL se comunica a través de puerto 5432.</span><span class="sxs-lookup"><span data-stu-id="9121a-158">Azure PostgreSQL server communicates over port 5432.</span></span> <span data-ttu-id="9121a-159">Si intenta conectarse desde una red corporativa, es posible que el firewall de la red no permita el tráfico saliente a través del puerto 5432.</span><span class="sxs-lookup"><span data-stu-id="9121a-159">If you are trying to connect from within a corporate network, outbound traffic over port 5432 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="9121a-160">Si es así, no podrá conectarse al servidor Azure SQL Database, a menos que el departamento de TI abra el puerto 5432.</span><span class="sxs-lookup"><span data-stu-id="9121a-160">If so, you will not be able to connect to your Azure SQL Database server unless your IT department opens port 5432.</span></span>
  >


## <a name="get-the-connection-information"></a><span data-ttu-id="9121a-161">Obtención de la información de conexión</span><span class="sxs-lookup"><span data-stu-id="9121a-161">Get the connection information</span></span>

<span data-ttu-id="9121a-162">Al crear el servidor de Azure Database for PostgreSQL, también se crea la base de datos de **postgres** predeterminada.</span><span class="sxs-lookup"><span data-stu-id="9121a-162">When we created our Azure Database for PostgreSQL server, the default **postgres** database also gets created.</span></span> <span data-ttu-id="9121a-163">Para conectarse al servidor de bases de datos, debe proporcionar las credenciales de acceso y la información del host.</span><span class="sxs-lookup"><span data-stu-id="9121a-163">To connect to your database server, you need to provide host information and access credentials.</span></span>

1. <span data-ttu-id="9121a-164">En el menú izquierdo de Azure Portal, haga clic en **Todos los recursos** y busque el servidor **mypgserver-20170401** que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="9121a-164">From the left-hand menu in Azure portal, click **All resources** and search for the server you just created **mypgserver-20170401**.</span></span>

  ![<span data-ttu-id="9121a-165">Azure Database for PostgreSQL: búsqueda de un servidor</span><span class="sxs-lookup"><span data-stu-id="9121a-165">Azure Database for PostgreSQL - Search for server</span></span> ](./media/tutorial-design-database-using-azure-portal/4-locate.png)

3. <span data-ttu-id="9121a-166">Haga clic en el nombre del servidor **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="9121a-166">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="9121a-167">Seleccione la página **Introducción** del servidor.</span><span class="sxs-lookup"><span data-stu-id="9121a-167">Select the server's **Overview** page.</span></span> <span data-ttu-id="9121a-168">Tome nota del **Nombre del servidor** y del **Server admin login name** (Nombre de inicio de sesión del administrador del servidor).</span><span class="sxs-lookup"><span data-stu-id="9121a-168">Make a note of the **Server name** and **Server admin login name**.</span></span>

 ![Azure Database for PostgreSQL: inicio de sesión del administrador del servidor](./media/tutorial-design-database-using-azure-portal/6-server-name.png)


## <a name="connect-to-postgresql-database-using-psql-in-cloud-shell"></a><span data-ttu-id="9121a-170">Conexión a la base de datos de PostgreSQL mediante psql de Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="9121a-170">Connect to PostgreSQL database using psql in Cloud Shell</span></span>

<span data-ttu-id="9121a-171">Ahora vamos a usar la utilidad de línea de comandos psql para conectarnos al servidor de Azure Database for PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="9121a-171">Let's now use the psql command-line utility to connect to the Azure Database for PostgreSQL server.</span></span> 
1. <span data-ttu-id="9121a-172">Inicie Azure Cloud Shell desde el icono del terminal en el panel de navegación superior.</span><span class="sxs-lookup"><span data-stu-id="9121a-172">Launch the Azure Cloud Shell via the terminal icon on the top navigation pane.</span></span>

   ![Azure Database for PostgreSQL: icono del terminal de Azure Cloud Shell](./media/tutorial-design-database-using-azure-portal/7-cloud-shell.png)

2. <span data-ttu-id="9121a-174">Azure Cloud Shell se abrirá en el explorador y podrá escribir comandos de Bash.</span><span class="sxs-lookup"><span data-stu-id="9121a-174">The Azure Cloud Shell opens in your browser, enabling you to type bash commands.</span></span>

   ![Azure Database for PostgreSQL: indicador de Bash de Azure Shell](./media/tutorial-design-database-using-azure-portal/8-bash.png)

3. <span data-ttu-id="9121a-176">En el símbolo de sistema de Cloud Shell, conéctese al servidor de Azure Database for PostgreSQL con los comandos psql.</span><span class="sxs-lookup"><span data-stu-id="9121a-176">At the Cloud Shell prompt, connect to your Azure Database for PostgreSQL server using the psql commands.</span></span> <span data-ttu-id="9121a-177">El formato siguiente sirve para conectarse a un servidor de Azure Database for PostgreSQL con la utilidad [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html):</span><span class="sxs-lookup"><span data-stu-id="9121a-177">The following format is used to connect to an Azure Database for PostgreSQL server with the [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility:</span></span>
   ```bash
   psql --host=<myserver> --port=<port> --username=<server admin login> --dbname=<database name>
   ```

   <span data-ttu-id="9121a-178">Por ejemplo, el siguiente comando se conecta a la base de datos predeterminada denominada **postgres** en el servidor PostgreSQL **mypgserver-20170401.postgres.database.azure.com** con las credenciales de acceso.</span><span class="sxs-lookup"><span data-stu-id="9121a-178">For example, the following command connects to the default database called **postgres** on your PostgreSQL server **mypgserver-20170401.postgres.database.azure.com** using access credentials.</span></span> <span data-ttu-id="9121a-179">Escriba la contraseña de administrador del servidor cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="9121a-179">Enter your server admin password when prompted.</span></span>

   ```bash
   psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=postgres
   ```

## <a name="create-a-new-database"></a><span data-ttu-id="9121a-180">Creación de una base de datos</span><span class="sxs-lookup"><span data-stu-id="9121a-180">Create a New Database</span></span>
<span data-ttu-id="9121a-181">Una vez conectado al servidor, cree una base de datos vacía en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="9121a-181">Once you're connected to the server, create a blank database at the prompt.</span></span>
```bash
CREATE DATABASE mypgsqldb;
```

<span data-ttu-id="9121a-182">En el símbolo del sistema, ejecute el siguiente comando para cambiar la conexión a la base de datos **mypgsqldb** recién creada.</span><span class="sxs-lookup"><span data-stu-id="9121a-182">At the prompt, execute the following command to switch connection to the newly created database **mypgsqldb**.</span></span>
```bash
\c mypgsqldb
```
## <a name="create-tables-in-the-database"></a><span data-ttu-id="9121a-183">Creación de tablas en la base de datos</span><span class="sxs-lookup"><span data-stu-id="9121a-183">Create tables in the database</span></span>
<span data-ttu-id="9121a-184">Ahora que sabe cómo conectarse a Azure Database for PostgreSQL, podemos ver cómo completar algunas tareas básicas.</span><span class="sxs-lookup"><span data-stu-id="9121a-184">Now that you know how to connect to the Azure Database for PostgreSQL, we can go over how to complete some basic tasks.</span></span>

<span data-ttu-id="9121a-185">En primer lugar, podemos crear una tabla y cargarla con algunos datos.</span><span class="sxs-lookup"><span data-stu-id="9121a-185">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="9121a-186">Vamos a crear una tabla que hace el seguimiento de información del inventario.</span><span class="sxs-lookup"><span data-stu-id="9121a-186">Let's create a table that tracks inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

<span data-ttu-id="9121a-187">Puede ver la tabla recién creada ahora en la lista de tablas si escribe lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="9121a-187">You can see the newly created table in the list of tabvles now by typing:</span></span>
```sql
\dt
```

## <a name="load-data-into-the-tables"></a><span data-ttu-id="9121a-188">Carga de datos en las tablas</span><span class="sxs-lookup"><span data-stu-id="9121a-188">Load data into the tables</span></span>
<span data-ttu-id="9121a-189">Ahora que tenemos una tabla, podemos insertar algunos datos en ella.</span><span class="sxs-lookup"><span data-stu-id="9121a-189">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="9121a-190">En la ventana de símbolo del sistema abierta, ejecute la consulta siguiente para insertar algunas filas de datos</span><span class="sxs-lookup"><span data-stu-id="9121a-190">At the open command prompt window, run the following query to insert some rows of data</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="9121a-191">Ahora tiene dos filas de datos de ejemplo en la tabla que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="9121a-191">You have now two rows of sample data into the table you created earlier.</span></span>

## <a name="query-and-update-the-data-in-the-tables"></a><span data-ttu-id="9121a-192">Consulta y actualización de los datos en las tablas</span><span class="sxs-lookup"><span data-stu-id="9121a-192">Query and update the data in the tables</span></span>
<span data-ttu-id="9121a-193">Ejecute la consulta siguiente para recuperar información de la tabla de base de datos.</span><span class="sxs-lookup"><span data-stu-id="9121a-193">Execute the following query to retrieve information from the database table.</span></span> 
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="9121a-194">También puede actualizar los datos en las tablas</span><span class="sxs-lookup"><span data-stu-id="9121a-194">You can also update the data in the tables</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="9121a-195">La fila se actualiza en consecuencia cuando se recuperan los datos.</span><span class="sxs-lookup"><span data-stu-id="9121a-195">The row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-data-to-a-previous-point-in-time"></a><span data-ttu-id="9121a-196">Restauración de datos a un momento dado anterior</span><span class="sxs-lookup"><span data-stu-id="9121a-196">Restore data to a previous point in time</span></span>
<span data-ttu-id="9121a-197">Imagine que eliminó accidentalmente esta tabla.</span><span class="sxs-lookup"><span data-stu-id="9121a-197">Imagine you have accidentally deleted this table.</span></span> <span data-ttu-id="9121a-198">No se puede recuperar con facilidad de esta situación.</span><span class="sxs-lookup"><span data-stu-id="9121a-198">This situation is something you cannot easily recover from.</span></span> <span data-ttu-id="9121a-199">Azure Database for PostgreSQL permite volver a cualquier momento dado en el período de los últimos 7 días (Básico) y los últimos 35 días (Estándar) y restaurar este momento dado en un servidor nuevo.</span><span class="sxs-lookup"><span data-stu-id="9121a-199">Azure Database for PostgreSQL allows you to go back to any point-in-time (in the last up to 7 days (Basic) and 35 days (Standard)) and restore this point-in-time to a new server.</span></span> <span data-ttu-id="9121a-200">Puede usar este servidor nuevo para recuperar los datos eliminados.</span><span class="sxs-lookup"><span data-stu-id="9121a-200">You can use this new server to recover your deleted data.</span></span> <span data-ttu-id="9121a-201">Los pasos siguientes restauran el servidor de ejemplo a un punto antes de que se agregara la tabla.</span><span class="sxs-lookup"><span data-stu-id="9121a-201">The following steps restore the sample server to a point before the table was added.</span></span>

1.  <span data-ttu-id="9121a-202">En la página Azure Database for PostgreSQL del servidor, haga clic en **Restaurar** en la barra de herramientas.</span><span class="sxs-lookup"><span data-stu-id="9121a-202">On the Azure Database for PostgreSQL page for your server, click **Restore** on the toolbar.</span></span> <span data-ttu-id="9121a-203">Se abre la página de **restauración**.</span><span class="sxs-lookup"><span data-stu-id="9121a-203">The **Restore** page opens.</span></span>
  <span data-ttu-id="9121a-204">![Azure Portal: opciones del formulario de restauración](./media/tutorial-design-database-using-azure-portal/9-azure-portal-restore.png)</span><span class="sxs-lookup"><span data-stu-id="9121a-204">![Azure portal - Restore form options](./media/tutorial-design-database-using-azure-portal/9-azure-portal-restore.png)</span></span>
2.  <span data-ttu-id="9121a-205">Rellene el formulario de **restauración** con la información necesaria:</span><span class="sxs-lookup"><span data-stu-id="9121a-205">Fill out the **Restore** form with the required information:</span></span>

  ![Azure Portal: opciones del formulario de restauración](./media/tutorial-design-database-using-azure-portal/10-azure-portal-restore.png)
  - <span data-ttu-id="9121a-207">**Punto de restauración**: seleccione el momento antes de que se modificara la base de datos</span><span class="sxs-lookup"><span data-stu-id="9121a-207">**Restore point**: Select a point-in-time that occurs before the server was changed</span></span>
  - <span data-ttu-id="9121a-208">**Servidor de destino**: especifique el nombre del nuevo servidor donde desea restaurar</span><span class="sxs-lookup"><span data-stu-id="9121a-208">**Target server**: Provide a new server name you want to restore to</span></span>
  - <span data-ttu-id="9121a-209">**Ubicación**: no se puede seleccionar la región; de forma predeterminada, es la misma que la del servidor de origen</span><span class="sxs-lookup"><span data-stu-id="9121a-209">**Location**: You cannot select the region, by default it is same as the source server</span></span>
  - <span data-ttu-id="9121a-210">**Plan de tarifa**: no se puede cambiar este valor al restaurar un servidor.</span><span class="sxs-lookup"><span data-stu-id="9121a-210">**Pricing tier**: You cannot change this value when restoring a server.</span></span> <span data-ttu-id="9121a-211">Es el mismo que el del servidor de origen.</span><span class="sxs-lookup"><span data-stu-id="9121a-211">It is same as the source server.</span></span> 
3.  <span data-ttu-id="9121a-212">Haga clic en **Aceptar** para restaurar el servidor a un [momento dado](./howto-restore-server-portal.md) antes de que se eliminaran las tablas.</span><span class="sxs-lookup"><span data-stu-id="9121a-212">Click **OK** to restore the server to [restore to a point-in-time](./howto-restore-server-portal.md) before the tables was deleted.</span></span> <span data-ttu-id="9121a-213">Restaurar un servidor a un momento dado distinto crea un servidor nuevo duplicado como el servidor original a partir del momento dado que especifique, siempre que se encuentren dentro del período de retención para el [nivel de servicio](./concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="9121a-213">Restoring a server to a different point in time creates a duplicate new server as the original server as of the point in time you specify, provided that it is within the retention period for your [service tier](./concepts-service-tiers.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9121a-214">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9121a-214">Next Steps</span></span>
<span data-ttu-id="9121a-215">En este tutorial, aprendió a usar Azure Portal y otras utilidades para hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="9121a-215">In this tutorial, you learned how to use the Azure portal and other utilities to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="9121a-216">Creación de una base de datos de Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="9121a-216">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="9121a-217">Configuración del firewall del servidor</span><span class="sxs-lookup"><span data-stu-id="9121a-217">Configure the server firewall</span></span>
> * <span data-ttu-id="9121a-218">Uso de la utilidad [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) para crear una base de datos</span><span class="sxs-lookup"><span data-stu-id="9121a-218">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility to create a database</span></span>
> * <span data-ttu-id="9121a-219">Carga de datos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="9121a-219">Load sample data</span></span>
> * <span data-ttu-id="9121a-220">Datos de consulta</span><span class="sxs-lookup"><span data-stu-id="9121a-220">Query data</span></span>
> * <span data-ttu-id="9121a-221">Actualización de datos</span><span class="sxs-lookup"><span data-stu-id="9121a-221">Update data</span></span>
> * <span data-ttu-id="9121a-222">Restauración de datos</span><span class="sxs-lookup"><span data-stu-id="9121a-222">Restore data</span></span>

<span data-ttu-id="9121a-223">A continuación, obtenga información sobre cómo usar la CLI de Azure para hacer tareas similares en el tutorial [Diseño de la primera base de datos de Azure Database for PostgreSQL con la CLI de Azure](tutorial-design-database-using-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="9121a-223">Next, learn how to use Azure CLI to do similar tasks, review this tutorial: [Design your first Azure Database for PostgreSQL using Azure CLI](tutorial-design-database-using-azure-cli.md)</span></span>
