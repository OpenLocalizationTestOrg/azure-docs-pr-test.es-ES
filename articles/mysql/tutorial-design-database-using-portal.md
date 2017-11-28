---
title: aaaDesign Azure primero la base de datos para la base de datos de MySQL - Portal de Azure | Documentos de Microsoft
description: "Este tutorial le explica cómo toocreate y administrar la base de datos de MySQL server y base de datos mediante el Portal de Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/06/2017
ms.custom: mvc
ms.openlocfilehash: 06dd952acc5356b8cccaf36917df1ff8db4f7139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a><span data-ttu-id="edad3-103">Diseño de la primera base de datos de Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="edad3-103">Design your first Azure Database for MySQL database</span></span>
<span data-ttu-id="edad3-104">Base de datos de Azure para MySQL es un servicio administrado que le permite toorun, administrar y escalar alta disponibilidad bases de datos MySQL en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="edad3-104">Azure Database for MySQL is a managed service that enables you toorun, manage, and scale highly available MySQL databases in hello cloud.</span></span> <span data-ttu-id="edad3-105">Con hello portal de Azure, puede administrar el servidor fácilmente y diseñar una base de datos.</span><span class="sxs-lookup"><span data-stu-id="edad3-105">Using hello Azure portal, you can easily manage your server and design a database.</span></span>

<span data-ttu-id="edad3-106">En este tutorial, utilice hello toolearn portal Azure cómo para:</span><span class="sxs-lookup"><span data-stu-id="edad3-106">In this tutorial, you use hello Azure portal toolearn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="edad3-107">Creación de una instancia de Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="edad3-107">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="edad3-108">Configurar firewall de servidor hello</span><span class="sxs-lookup"><span data-stu-id="edad3-108">Configure hello server firewall</span></span>
> * <span data-ttu-id="edad3-109">Use la herramienta de línea de comandos de mysql toocreate una base de datos</span><span class="sxs-lookup"><span data-stu-id="edad3-109">Use mysql command-line tool toocreate a database</span></span>
> * <span data-ttu-id="edad3-110">Carga de datos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="edad3-110">Load sample data</span></span>
> * <span data-ttu-id="edad3-111">Datos de consulta</span><span class="sxs-lookup"><span data-stu-id="edad3-111">Query data</span></span>
> * <span data-ttu-id="edad3-112">Actualización de datos</span><span class="sxs-lookup"><span data-stu-id="edad3-112">Update data</span></span>
> * <span data-ttu-id="edad3-113">Restauración de datos</span><span class="sxs-lookup"><span data-stu-id="edad3-113">Restore data</span></span>

## <a name="sign-in-toohello-azure-portal"></a><span data-ttu-id="edad3-114">Inicie sesión en toohello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="edad3-114">Sign in toohello Azure portal</span></span>
<span data-ttu-id="edad3-115">Abra el explorador web favoritas y visite hello [portal de Microsoft Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="edad3-115">Open your favorite web browser, and visit hello [Microsoft Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="edad3-116">Escriba su credenciales toosign en toohello portal.</span><span class="sxs-lookup"><span data-stu-id="edad3-116">Enter your credentials toosign in toohello portal.</span></span> <span data-ttu-id="edad3-117">vista predeterminada de Hello es el panel de servicio.</span><span class="sxs-lookup"><span data-stu-id="edad3-117">hello default view is your service dashboard.</span></span>

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="edad3-118">Creación de un servidor de Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="edad3-118">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="edad3-119">Se crea un servidor de Azure Database for MySQL con un conjunto definido de [recursos de proceso y almacenamiento](./concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="edad3-119">An Azure Database for MySQL server is created with a defined set of [compute and storage resources](./concepts-compute-unit-and-storage.md).</span></span> <span data-ttu-id="edad3-120">servidor de Hola se crea dentro de un [grupo de recursos de Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span><span class="sxs-lookup"><span data-stu-id="edad3-120">hello server is created within an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span></span>

1. <span data-ttu-id="edad3-121">Navegue demasiado**bases de datos** > **base de datos de Azure para MySQL**.</span><span class="sxs-lookup"><span data-stu-id="edad3-121">Navigate too**Databases** > **Azure Database for MySQL**.</span></span> <span data-ttu-id="edad3-122">Si no se puede encontrar el servidor de MySQL en **bases de datos** categoría, haga clic en **ver todas** tooshow disponible todos los servicios de base de datos.</span><span class="sxs-lookup"><span data-stu-id="edad3-122">If you cannot find MySQL Server under **Databases** category, click **See all** tooshow all available database services.</span></span> <span data-ttu-id="edad3-123">También puede escribir **base de datos de Azure para MySQL** en tooquickly de cuadro de búsqueda de hello busque servicio Hola.</span><span class="sxs-lookup"><span data-stu-id="edad3-123">You can also type **Azure Database for MySQL** in hello search box tooquickly find hello service.</span></span>
<span data-ttu-id="edad3-124">![2-1 Navigate tooMySQL](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)</span><span class="sxs-lookup"><span data-stu-id="edad3-124">![2-1 Navigate tooMySQL](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)</span></span>

2. <span data-ttu-id="edad3-125">Haga clic en el icono **Azure Database for MySQL** y, después, en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="edad3-125">Click **Azure Database for MySQL** tile, and then click **Create**.</span></span>

<span data-ttu-id="edad3-126">En nuestro ejemplo, rellene Hola base de datos de Azure para el formulario de MySQL con hello siguiente información:</span><span class="sxs-lookup"><span data-stu-id="edad3-126">In our example, fill out hello Azure Database for MySQL form with hello following information:</span></span>

| <span data-ttu-id="edad3-127">**Configuración**</span><span class="sxs-lookup"><span data-stu-id="edad3-127">**Setting**</span></span> | <span data-ttu-id="edad3-128">**Valor sugerido**</span><span class="sxs-lookup"><span data-stu-id="edad3-128">**Suggested value**</span></span> | <span data-ttu-id="edad3-129">**Descripción del campo**</span><span class="sxs-lookup"><span data-stu-id="edad3-129">**Field Description**</span></span> |
|---|---|---|
| <span data-ttu-id="edad3-130">*Nombre del servidor*</span><span class="sxs-lookup"><span data-stu-id="edad3-130">*Server name*</span></span> | <span data-ttu-id="edad3-131">myserver4demo</span><span class="sxs-lookup"><span data-stu-id="edad3-131">myserver4demo</span></span>  | <span data-ttu-id="edad3-132">Nombre del servidor tiene toobe único global.</span><span class="sxs-lookup"><span data-stu-id="edad3-132">Server name has toobe globally unique.</span></span> |
| <span data-ttu-id="edad3-133">*Suscripción*</span><span class="sxs-lookup"><span data-stu-id="edad3-133">*Subscription*</span></span> | <span data-ttu-id="edad3-134">mysubscription</span><span class="sxs-lookup"><span data-stu-id="edad3-134">mysubscription</span></span> | <span data-ttu-id="edad3-135">Seleccione la suscripción en Hola de lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="edad3-135">Select your subscription from hello drop-down.</span></span> |
| <span data-ttu-id="edad3-136">*Grupos de recursos*</span><span class="sxs-lookup"><span data-stu-id="edad3-136">*Resource group*</span></span> | <span data-ttu-id="edad3-137">myresourcegroup</span><span class="sxs-lookup"><span data-stu-id="edad3-137">myresourcegroup</span></span> | <span data-ttu-id="edad3-138">Cree un grupo de recursos o use uno existente.</span><span class="sxs-lookup"><span data-stu-id="edad3-138">Create a resource group or use an existing one.</span></span> |
| <span data-ttu-id="edad3-139">*Inicio de sesión del administrador del servidor*</span><span class="sxs-lookup"><span data-stu-id="edad3-139">*Server admin login*</span></span> | <span data-ttu-id="edad3-140">myadmin</span><span class="sxs-lookup"><span data-stu-id="edad3-140">myadmin</span></span> | <span data-ttu-id="edad3-141">Nombre de la cuenta de administrador de configuración.</span><span class="sxs-lookup"><span data-stu-id="edad3-141">Setup admin account name.</span></span> |
| <span data-ttu-id="edad3-142">*Password*</span><span class="sxs-lookup"><span data-stu-id="edad3-142">*Password*</span></span> |  | <span data-ttu-id="edad3-143">Configure una contraseña de la cuenta de administrador segura.</span><span class="sxs-lookup"><span data-stu-id="edad3-143">Set a strong admin account password.</span></span> |
| <span data-ttu-id="edad3-144">*Confirmar contraseña*</span><span class="sxs-lookup"><span data-stu-id="edad3-144">*Confirm password*</span></span> |  | <span data-ttu-id="edad3-145">Confirme la contraseña de cuenta de administrador de Hola.</span><span class="sxs-lookup"><span data-stu-id="edad3-145">Confirm hello admin account password.</span></span> |
| <span data-ttu-id="edad3-146">*Ubicación*</span><span class="sxs-lookup"><span data-stu-id="edad3-146">*Location*</span></span> |  | <span data-ttu-id="edad3-147">Seleccione una región disponible.</span><span class="sxs-lookup"><span data-stu-id="edad3-147">Select an available region.</span></span> |
| <span data-ttu-id="edad3-148">*Versión*</span><span class="sxs-lookup"><span data-stu-id="edad3-148">*Version*</span></span> | <span data-ttu-id="edad3-149">5.7</span><span class="sxs-lookup"><span data-stu-id="edad3-149">5.7</span></span> | <span data-ttu-id="edad3-150">Elija la versión más reciente de Hola.</span><span class="sxs-lookup"><span data-stu-id="edad3-150">Choose hello latest version.</span></span> |
| <span data-ttu-id="edad3-151">*Configurar rendimiento*</span><span class="sxs-lookup"><span data-stu-id="edad3-151">*Configure performance*</span></span> | <span data-ttu-id="edad3-152">Básico, 50 unidades de proceso, 50 GB</span><span class="sxs-lookup"><span data-stu-id="edad3-152">Basic, 50 compute units, 50 GB</span></span>  | <span data-ttu-id="edad3-153">Seleccione **Plan de tarifa**, **Unidades de proceso**, **Almacenamiento (GB)** y, finalmente, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="edad3-153">Choose **Pricing tier**, **Compute Units**, **Storage (GB)**, and then click **OK**.</span></span> |
| <span data-ttu-id="edad3-154">*TooDashboard de PIN*</span><span class="sxs-lookup"><span data-stu-id="edad3-154">*Pin tooDashboard*</span></span> | <span data-ttu-id="edad3-155">Comprobar</span><span class="sxs-lookup"><span data-stu-id="edad3-155">Check</span></span> | <span data-ttu-id="edad3-156">Recomienda toocheck esta casilla para que puede encontrar fácilmente más adelante en servidor hello</span><span class="sxs-lookup"><span data-stu-id="edad3-156">Recommended toocheck this box so you may find hello server easily later on</span></span> |
<span data-ttu-id="edad3-157">A continuación, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="edad3-157">Then, click **Create**.</span></span> <span data-ttu-id="edad3-158">En un minuto o dos, una nueva base de datos de Azure para servidor MySQL se está ejecutando en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="edad3-158">In a minute or two, a new Azure Database for MySQL server is running in hello cloud.</span></span> <span data-ttu-id="edad3-159">Puede hacer clic en **notificaciones** botón en el proceso de implementación de hello barra de herramientas toomonitor Hola.</span><span class="sxs-lookup"><span data-stu-id="edad3-159">You can click **Notifications** button on hello toolbar toomonitor hello deployment process.</span></span>

## <a name="configure-firewall"></a><span data-ttu-id="edad3-160">Configuración del firewall</span><span class="sxs-lookup"><span data-stu-id="edad3-160">Configure firewall</span></span>
<span data-ttu-id="edad3-161">Las bases de datos de Azure para MySQL están protegidas con un firewall.</span><span class="sxs-lookup"><span data-stu-id="edad3-161">Azure Databases for MySQL are protected by a firewall.</span></span> <span data-ttu-id="edad3-162">De forma predeterminada, se rechazan todas las conexiones toohello hello y servidor de bases de datos dentro de servidor hello.</span><span class="sxs-lookup"><span data-stu-id="edad3-162">By default, all connections toohello server and hello databases inside hello server are rejected.</span></span> <span data-ttu-id="edad3-163">Antes de conectarse tooAzure base de datos MySQL para hello primera vez, configure la dirección IP de red pública de la máquina de hello firewall tooadd Hola cliente (o intervalo de direcciones IP).</span><span class="sxs-lookup"><span data-stu-id="edad3-163">Before connecting tooAzure Database for MySQL for hello first time, configure hello firewall tooadd hello client machine's public network IP address (or IP address range).</span></span>

1. <span data-ttu-id="edad3-164">Haga clic en el servidor recién creado y, luego, en **Seguridad de la conexión**.</span><span class="sxs-lookup"><span data-stu-id="edad3-164">Click your newly created server, and then click **Connection security**.</span></span>
   <span data-ttu-id="edad3-165">![3-1 Seguridad de conexión](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)</span><span class="sxs-lookup"><span data-stu-id="edad3-165">![3-1 Connection security](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)</span></span>
2. <span data-ttu-id="edad3-166">Puede **agregar su dirección IP** o configurar aquí las reglas de firewall.</span><span class="sxs-lookup"><span data-stu-id="edad3-166">You can **Add My IP**, or configure firewall rules here.</span></span> <span data-ttu-id="edad3-167">Recuerde tooclick **guardar** después de haber creado reglas Hola.</span><span class="sxs-lookup"><span data-stu-id="edad3-167">Remember tooclick **Save** after you have created hello rules.</span></span>
<span data-ttu-id="edad3-168">Ahora puede conectarse server toohello mediante la herramienta de línea de comandos de mysql o herramienta de interfaz gráfica de usuario de MySQL Workbench.</span><span class="sxs-lookup"><span data-stu-id="edad3-168">You can now connect toohello server using mysql command-line tool or MySQL Workbench GUI tool.</span></span>

> [!TIP]
> <span data-ttu-id="edad3-169">El servidor de Azure Database for MySQL se comunica a través del puerto 3306.</span><span class="sxs-lookup"><span data-stu-id="edad3-169">Azure Database for MySQL server communicates over port 3306.</span></span> <span data-ttu-id="edad3-170">Si está tratando de tooconnect desde dentro de una red corporativa, es posible que firewall de su red no permite el tráfico saliente en el puerto 3306.</span><span class="sxs-lookup"><span data-stu-id="edad3-170">If you are trying tooconnect from within a corporate network, outbound traffic over port 3306 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="edad3-171">Si es así, no se puede conectar tooAzure MySQL server a menos que el departamento de TI abre el puerto 3306.</span><span class="sxs-lookup"><span data-stu-id="edad3-171">If so, you cannot connect tooAzure MySQL server unless your IT department opens port 3306.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="edad3-172">Obtención de información sobre la conexión</span><span class="sxs-lookup"><span data-stu-id="edad3-172">Get connection information</span></span>
<span data-ttu-id="edad3-173">Hola Get completo **nombre del servidor** y **nombre de inicio de sesión del Administrador de servidor** para la base de datos de Azure para servidor de MySQL de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="edad3-173">Get hello fully qualified **Server name** and **Server admin login name** for your Azure Database for MySQL server from hello Azure portal.</span></span> <span data-ttu-id="edad3-174">Usa Hola completo nombre tooconnect tooyour server mediante la herramienta de línea de comandos de mysql.</span><span class="sxs-lookup"><span data-stu-id="edad3-174">You use hello fully qualified server name tooconnect tooyour server using mysql command-line tool.</span></span> 

1. <span data-ttu-id="edad3-175">En [portal de Azure](https://portal.azure.com/), haga clic en **todos los recursos** desde el menú izquierdo hello, nombre de tipo hello y busque la base de datos de Azure para servidor MySQL.</span><span class="sxs-lookup"><span data-stu-id="edad3-175">In [Azure portal](https://portal.azure.com/), click **All resources** from hello left-hand menu, type hello name, and search for your Azure Database for MySQL server.</span></span> <span data-ttu-id="edad3-176">Seleccione detalles hello tooview nombre del servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="edad3-176">Select hello server name tooview hello details.</span></span>

2. <span data-ttu-id="edad3-177">En configuración de hello encabezado, haga clic en **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="edad3-177">Under hello Settings heading, click **Properties**.</span></span> <span data-ttu-id="edad3-178">Anote los valores de **NOMBRE DEL SERVIDOR** y **NOMBRE DE INICIO DE SESIÓN DEL ADMINISTRADOR DEL SERVIDOR**.</span><span class="sxs-lookup"><span data-stu-id="edad3-178">Note down **SERVER NAME** and **SERVER ADMIN LOGIN NAME**.</span></span> <span data-ttu-id="edad3-179">Puede hacer clic en hello Copiar botón siguiente tooeach campo toocopy toohello Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="edad3-179">You may click hello copy button next tooeach field toocopy toohello clipboard.</span></span>
   <span data-ttu-id="edad3-180">![4-2 Propiedades del servidor](./media/tutorial-design-database-using-portal/4_2-server-properties.png)</span><span class="sxs-lookup"><span data-stu-id="edad3-180">![4-2 server properties](./media/tutorial-design-database-using-portal/4_2-server-properties.png)</span></span>

<span data-ttu-id="edad3-181">En este ejemplo, es el nombre del servidor de hello *myserver4demo.mysql.database.azure.com*, y es el inicio de sesión de administrador de servidor de hello  *myadmin@myserver4demo* .</span><span class="sxs-lookup"><span data-stu-id="edad3-181">In this example, hello server name is *myserver4demo.mysql.database.azure.com*, and hello server admin login is *myadmin@myserver4demo*.</span></span>

## <a name="connect-toohello-server-using-mysql"></a><span data-ttu-id="edad3-182">Conectar con mysql de servidor de toohello</span><span class="sxs-lookup"><span data-stu-id="edad3-182">Connect toohello server using mysql</span></span>
<span data-ttu-id="edad3-183">Use [herramienta de línea de comandos de mysql](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) tooestablish una tooyour de conexión base de datos de MySQL server.</span><span class="sxs-lookup"><span data-stu-id="edad3-183">Use [mysql command-line tool](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) tooestablish a connection tooyour Azure Database for MySQL server.</span></span> <span data-ttu-id="edad3-184">Puede ejecutar herramienta de línea de comandos de mysql Hola de hello Shell en la nube de Azure en el Explorador de Hola o de su propia máquina mediante herramientas de mysql instaladas de forma local.</span><span class="sxs-lookup"><span data-stu-id="edad3-184">You can run hello mysql command-line tool from hello Azure Cloud Shell in hello browser or from your own machine using mysql tools installed locally.</span></span> <span data-ttu-id="edad3-185">Hola toolaunch Shell en la nube de Azure, haga clic en hello `Try It` situado en un bloque de código en este artículo, o visite Hola portal de Azure y haga clic en hello `>_` icono en la barra de herramientas derecha Hola superior.</span><span class="sxs-lookup"><span data-stu-id="edad3-185">toolaunch hello Azure Cloud Shell, click hello `Try It` button on a code block in this article, or visit hello Azure portal and click hello `>_` icon in hello top right toolbar.</span></span> 

<span data-ttu-id="edad3-186">Escriba Hola comando tooconnect:</span><span class="sxs-lookup"><span data-stu-id="edad3-186">Type hello command tooconnect:</span></span>
```azurecli-interactive
mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

## <a name="create-a-blank-database"></a><span data-ttu-id="edad3-187">Crear una base de datos en blanco</span><span class="sxs-lookup"><span data-stu-id="edad3-187">Create a blank database</span></span>
<span data-ttu-id="edad3-188">Una vez que esté conectado toohello server, cree un toowork de base de datos en blanco con.</span><span class="sxs-lookup"><span data-stu-id="edad3-188">Once you’re connected toohello server, create a blank database toowork with.</span></span>
```sql
CREATE DATABASE mysampledb;
```

<span data-ttu-id="edad3-189">En el símbolo del sistema de hello, ejecute hello después de la base de datos de comando tooswitch conexión toothis recién creado:</span><span class="sxs-lookup"><span data-stu-id="edad3-189">At hello prompt, run hello following command tooswitch connection toothis newly created database:</span></span>
```sql
USE mysampledb;
```

## <a name="create-tables-in-hello-database"></a><span data-ttu-id="edad3-190">Crear tablas de base de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="edad3-190">Create tables in hello database</span></span>
<span data-ttu-id="edad3-191">Ahora que sabe cómo tooconnect toohello base de datos de Azure para la base de datos MySQL, podemos ver cómo toocomplete algunas tareas básicas.</span><span class="sxs-lookup"><span data-stu-id="edad3-191">Now that you know how tooconnect toohello Azure Database for MySQL database, we can go over how toocomplete some basic tasks.</span></span>

<span data-ttu-id="edad3-192">En primer lugar, podemos crear una tabla y cargarla con algunos datos.</span><span class="sxs-lookup"><span data-stu-id="edad3-192">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="edad3-193">Vamos a crear una tabla que almacena la información del inventario.</span><span class="sxs-lookup"><span data-stu-id="edad3-193">Let's create a table that stores inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-hello-tables"></a><span data-ttu-id="edad3-194">Cargar datos en tablas de Hola</span><span class="sxs-lookup"><span data-stu-id="edad3-194">Load data into hello tables</span></span>
<span data-ttu-id="edad3-195">Ahora que tenemos una tabla, podemos insertar algunos datos en ella.</span><span class="sxs-lookup"><span data-stu-id="edad3-195">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="edad3-196">En la ventana de símbolo del sistema abierto hello, ejecute hello después consulta tooinsert algunas filas de datos.</span><span class="sxs-lookup"><span data-stu-id="edad3-196">At hello open command prompt window, run hello following query tooinsert some rows of data.</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="edad3-197">Ahora tiene dos filas de datos de ejemplo en la tabla de Hola que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="edad3-197">Now you have two rows of sample data into hello table you created earlier.</span></span>

## <a name="query-and-update-hello-data-in-hello-tables"></a><span data-ttu-id="edad3-198">Consultar y actualizar los datos de hello en tablas de Hola</span><span class="sxs-lookup"><span data-stu-id="edad3-198">Query and update hello data in hello tables</span></span>
<span data-ttu-id="edad3-199">Ejecute hello siguientes tooretrieve información de consulta de tabla de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="edad3-199">Execute hello following query tooretrieve information from hello database table.</span></span>
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="edad3-200">También puede actualizar los datos de hello en tablas de Hola.</span><span class="sxs-lookup"><span data-stu-id="edad3-200">You can also update hello data in hello tables.</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="edad3-201">fila de Hola se actualiza en consecuencia cuando se recuperan datos.</span><span class="sxs-lookup"><span data-stu-id="edad3-201">hello row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a><span data-ttu-id="edad3-202">Restaurar un punto anterior de tooa de base de datos en el tiempo</span><span class="sxs-lookup"><span data-stu-id="edad3-202">Restore a database tooa previous point in time</span></span>
<span data-ttu-id="edad3-203">Imagine que ha eliminado accidentalmente una tabla de base de datos importantes y no puede recuperar datos de hello fácilmente.</span><span class="sxs-lookup"><span data-stu-id="edad3-203">Imagine you have accidentally deleted an important database table, and cannot recover hello data easily.</span></span> <span data-ttu-id="edad3-204">Base de datos de Azure para MySQL permite toorestore Hola server tooa punto en el tiempo, crear una copia de las bases de datos de hello en el nuevo servidor.</span><span class="sxs-lookup"><span data-stu-id="edad3-204">Azure Database for MySQL allows you toorestore hello server tooa point in time, creating a copy of hello databases into new server.</span></span> <span data-ttu-id="edad3-205">Puede usar esta nueva toorecover server los datos eliminados.</span><span class="sxs-lookup"><span data-stu-id="edad3-205">You can use this new server toorecover your deleted data.</span></span> <span data-ttu-id="edad3-206">Hola siguiendo los pasos restauración Hola ejemplo servidor tooa punto antes de que se ha agregado Hola tabla.</span><span class="sxs-lookup"><span data-stu-id="edad3-206">hello following steps restore hello sample server tooa point before hello table was added.</span></span>

1. <span data-ttu-id="edad3-207">Hola portal de Azure, busque la base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="edad3-207">In hello Azure portal, locate your Azure Database for MySQL.</span></span> <span data-ttu-id="edad3-208">En hello **Introducción** página, haga clic en **restaurar** en la barra de herramientas de Hola.</span><span class="sxs-lookup"><span data-stu-id="edad3-208">On hello **Overview** page, click **Restore** on hello toolbar.</span></span> <span data-ttu-id="edad3-209">se abre la página de la restauración de Hola.</span><span class="sxs-lookup"><span data-stu-id="edad3-209">hello Restore page opens.</span></span>

   ![10-1 Restaurar una base de datos](./media/tutorial-design-database-using-portal/10_1-restore-a-db.png)

2. <span data-ttu-id="edad3-211">Rellene hello **restaurar** formulario con la información de hello necesario.</span><span class="sxs-lookup"><span data-stu-id="edad3-211">Fill out hello **Restore** form with hello required information.</span></span>
   
   ![10-2 Formulario de restauración](./media/tutorial-design-database-using-portal/10_2-restore-form.png)
   
   - <span data-ttu-id="edad3-213">**Punto de restauración**: seleccione un punto-in-time que desea toorestore, plazo Hola enumerados.</span><span class="sxs-lookup"><span data-stu-id="edad3-213">**Restore point**: Select a point-in-time that you want toorestore to, within hello timeframe listed.</span></span> <span data-ttu-id="edad3-214">Asegúrese de tooconvert seguro su tooUTC de zona horaria local.</span><span class="sxs-lookup"><span data-stu-id="edad3-214">Make sure tooconvert your local timezone tooUTC.</span></span>
   - <span data-ttu-id="edad3-215">**Restaurar el servidor de toonew**: especifique un nuevo nombre de servidor que desee toorestore a.</span><span class="sxs-lookup"><span data-stu-id="edad3-215">**Restore toonew server**: Provide a new server name you want toorestore to.</span></span>
   - <span data-ttu-id="edad3-216">**Ubicación**: Hola región es el mismo que el servidor de origen de hello y no se puede cambiar.</span><span class="sxs-lookup"><span data-stu-id="edad3-216">**Location**: hello region is same as hello source server, and cannot be changed.</span></span>
   - <span data-ttu-id="edad3-217">**Nivel de precios**: Hola tarifa es hello igual Hola servidor de origen y no se puede cambiar.</span><span class="sxs-lookup"><span data-stu-id="edad3-217">**Pricing tier**: hello pricing tier is hello same as hello source server, and cannot be changed.</span></span>
   
3. <span data-ttu-id="edad3-218">Haga clic en **Aceptar** toorestore Hola servidor demasiado[tooa punto de restauración tiempo](./howto-restore-server-portal.md) antes de que se eliminó la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="edad3-218">Click **OK** toorestore hello server too[restore tooa point in time](./howto-restore-server-portal.md) before hello table was deleted.</span></span> <span data-ttu-id="edad3-219">Restaurar un servidor, crea una nueva copia del servidor, hello, desde el punto de hello en el tiempo que especifique.</span><span class="sxs-lookup"><span data-stu-id="edad3-219">Restoring a server creates a new copy of hello server, as of hello point in time you specify.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="edad3-220">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="edad3-220">Next steps</span></span>
<span data-ttu-id="edad3-221">En este tutorial, utilice hello toolearned portal Azure cómo para:</span><span class="sxs-lookup"><span data-stu-id="edad3-221">In this tutorial, you use hello Azure portal toolearned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="edad3-222">Creación de una instancia de Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="edad3-222">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="edad3-223">Configurar firewall de servidor hello</span><span class="sxs-lookup"><span data-stu-id="edad3-223">Configure hello server firewall</span></span>
> * <span data-ttu-id="edad3-224">Use la herramienta de línea de comandos de mysql toocreate una base de datos</span><span class="sxs-lookup"><span data-stu-id="edad3-224">Use mysql command-line tool toocreate a database</span></span>
> * <span data-ttu-id="edad3-225">Carga de datos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="edad3-225">Load sample data</span></span>
> * <span data-ttu-id="edad3-226">Datos de consulta</span><span class="sxs-lookup"><span data-stu-id="edad3-226">Query data</span></span>
> * <span data-ttu-id="edad3-227">Actualización de datos</span><span class="sxs-lookup"><span data-stu-id="edad3-227">Update data</span></span>
> * <span data-ttu-id="edad3-228">Restauración de datos</span><span class="sxs-lookup"><span data-stu-id="edad3-228">Restore data</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="edad3-229">Cómo tooconnect tooAzure de las aplicaciones de base de datos de MySQL</span><span class="sxs-lookup"><span data-stu-id="edad3-229">How tooconnect applications tooAzure Database for MySQL</span></span>](./howto-connection-string.md)
