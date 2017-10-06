---
title: "aaaBuild una aplicación web PHP y MySQL en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooget una aplicación PHP trabajando en Azure, con conexión tooa MySQL de base de datos en Azure."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 14feb4f3-5095-496e-9a40-690e1414bd73
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 07/21/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 3c050b30e2e2c80d011bed989cd5f8cecac35d15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-php-and-mysql-web-app-in-azure"></a><span data-ttu-id="57378-103">Compilación de una aplicación web PHP y MySQL en Azure</span><span class="sxs-lookup"><span data-stu-id="57378-103">Build a PHP and MySQL web app in Azure</span></span>

<span data-ttu-id="57378-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) proporciona un servicio de hospedaje web muy escalable y con aplicación de revisiones de un modo automático.</span><span class="sxs-lookup"><span data-stu-id="57378-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="57378-105">Este tutorial muestra cómo toocreate un PHP web de aplicación en Azure y conectar tooa base de datos de MySQL.</span><span class="sxs-lookup"><span data-stu-id="57378-105">This tutorial shows how toocreate a PHP web app in Azure and connect it tooa MySQL database.</span></span> <span data-ttu-id="57378-106">Cuando haya terminado, tendrá una aplicación [Laravel](https://laravel.com/) que se ejecuta en Azure App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="57378-106">When you're finished, you'll have a [Laravel](https://laravel.com/) app running on Azure App Service Web Apps.</span></span>

![Aplicación PHP que se ejecuta en Azure App Service](./media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

<span data-ttu-id="57378-108">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="57378-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="57378-109">Crear una base de datos MySQL en Azure</span><span class="sxs-lookup"><span data-stu-id="57378-109">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="57378-110">Conectar un tooMySQL de aplicación PHP</span><span class="sxs-lookup"><span data-stu-id="57378-110">Connect a PHP app tooMySQL</span></span>
> * <span data-ttu-id="57378-111">Implementar Hola aplicación tooAzure</span><span class="sxs-lookup"><span data-stu-id="57378-111">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="57378-112">Actualizar el modelo de datos de Hola y volver a implementar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="57378-112">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="57378-113">Transmitir registros de diagnóstico desde Azure</span><span class="sxs-lookup"><span data-stu-id="57378-113">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="57378-114">Administrar aplicación Hola Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="57378-114">Manage hello app in hello Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57378-115">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="57378-115">Prerequisites</span></span>

<span data-ttu-id="57378-116">toocomplete este tutorial:</span><span class="sxs-lookup"><span data-stu-id="57378-116">toocomplete this tutorial:</span></span>

* [<span data-ttu-id="57378-117">Instalación de Git</span><span class="sxs-lookup"><span data-stu-id="57378-117">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="57378-118">Instalación de PHP 5.6.4, o cualquier versión posterior</span><span class="sxs-lookup"><span data-stu-id="57378-118">Install PHP 5.6.4 or above</span></span>](http://php.net/downloads.php)
* [<span data-ttu-id="57378-119">Instalación de Composer</span><span class="sxs-lookup"><span data-stu-id="57378-119">Install Composer</span></span>](https://getcomposer.org/doc/00-intro.md)
* <span data-ttu-id="57378-120">Habilitar Hola siguiendo las extensiones PHP necesidades Laravel: OpenSSL, MySQL PDO, Mbstring, Tokenizer, XML</span><span class="sxs-lookup"><span data-stu-id="57378-120">Enable hello following PHP extensions Laravel needs: OpenSSL, PDO-MySQL, Mbstring, Tokenizer, XML</span></span>
* [<span data-ttu-id="57378-121">Instalación e inicio de MySQL</span><span class="sxs-lookup"><span data-stu-id="57378-121">Install and start MySQL</span></span>](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prepare-local-mysql"></a><span data-ttu-id="57378-122">Preparación de MySQL local</span><span class="sxs-lookup"><span data-stu-id="57378-122">Prepare local MySQL</span></span>

<span data-ttu-id="57378-123">En este paso, creará una base de datos en el servidor MySQL local para usarlo en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="57378-123">In this step, you create a database in your local MySQL server for your use in this tutorial.</span></span>

### <a name="connect-toolocal-mysql-server"></a><span data-ttu-id="57378-124">Conectar toolocal MySQL server</span><span class="sxs-lookup"><span data-stu-id="57378-124">Connect toolocal MySQL server</span></span>

<span data-ttu-id="57378-125">En una ventana de terminal, conéctese tooyour local MySQL server.</span><span class="sxs-lookup"><span data-stu-id="57378-125">In a terminal window, connect tooyour local MySQL server.</span></span> <span data-ttu-id="57378-126">Puede utilizar esta ventana de terminal toorun todos los comandos de hello en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="57378-126">You can use this terminal window toorun all hello commands in this tutorial.</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="57378-127">Si se le pide una contraseña, escriba contraseña Hola de hello `root` cuenta.</span><span class="sxs-lookup"><span data-stu-id="57378-127">If you're prompted for a password, enter hello password for hello `root` account.</span></span> <span data-ttu-id="57378-128">Si no recuerda su contraseña de la cuenta raíz, consulte [MySQL: cómo tooReset Hola contraseña raíz](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span><span class="sxs-lookup"><span data-stu-id="57378-128">If you don't remember your root account password, see [MySQL: How tooReset hello Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span></span>

<span data-ttu-id="57378-129">Si el comando se ejecuta correctamente, significa que el servidor MySQL está en ejecución.</span><span class="sxs-lookup"><span data-stu-id="57378-129">If your command runs successfully, then your MySQL server is running.</span></span> <span data-ttu-id="57378-130">Si no es así, asegúrese de que el servidor MySQL local debe iniciarse mediante Hola siguiente [pasos posteriores a la instalación de MySQL](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span><span class="sxs-lookup"><span data-stu-id="57378-130">If not, make sure that your local MySQL server is started by following hello [MySQL post-installation steps](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span></span>

### <a name="create-a-database-locally"></a><span data-ttu-id="57378-131">Creación de una base de datos local</span><span class="sxs-lookup"><span data-stu-id="57378-131">Create a database locally</span></span>

<span data-ttu-id="57378-132">En hello `mysql` símbolo del sistema, cree una base de datos.</span><span class="sxs-lookup"><span data-stu-id="57378-132">At hello `mysql` prompt, create a database.</span></span>

```sql 
CREATE DATABASE sampledb;
```

<span data-ttu-id="57378-133">Escriba `quit` para salir de la conexión del servidor.</span><span class="sxs-lookup"><span data-stu-id="57378-133">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

<a name="step2"></a>

## <a name="create-a-php-app-locally"></a><span data-ttu-id="57378-134">Creación de una aplicación PHP local</span><span class="sxs-lookup"><span data-stu-id="57378-134">Create a PHP app locally</span></span>
<span data-ttu-id="57378-135">En este paso, obtendrá una aplicación Laravel de ejemplo, configurará la conexión a base de datos correspondiente y la ejecutará de forma local.</span><span class="sxs-lookup"><span data-stu-id="57378-135">In this step, you get a Laravel sample application, configure its database connection, and run it locally.</span></span> 

### <a name="clone-hello-sample"></a><span data-ttu-id="57378-136">Ejemplo de Hola de clon</span><span class="sxs-lookup"><span data-stu-id="57378-136">Clone hello sample</span></span>

<span data-ttu-id="57378-137">En la ventana de terminal de hello, `cd` tooa directorio de trabajo.</span><span class="sxs-lookup"><span data-stu-id="57378-137">In hello terminal window, `cd` tooa working directory.</span></span>

<span data-ttu-id="57378-138">Ejecute hello después de repositorio de ejemplo de comando tooclone Hola.</span><span class="sxs-lookup"><span data-stu-id="57378-138">Run hello following command tooclone hello sample repository.</span></span>

```bash
git clone https://github.com/Azure-Samples/laravel-tasks
```

<span data-ttu-id="57378-139">`cd`tooyour directorio clonado.</span><span class="sxs-lookup"><span data-stu-id="57378-139">`cd` tooyour cloned directory.</span></span>
<span data-ttu-id="57378-140">Instalar paquetes de saludo necesario.</span><span class="sxs-lookup"><span data-stu-id="57378-140">Install hello required packages.</span></span>

```bash
cd laravel-tasks
composer install
```

### <a name="configure-mysql-connection"></a><span data-ttu-id="57378-141">Configuración de la conexión a MySQL</span><span class="sxs-lookup"><span data-stu-id="57378-141">Configure MySQL connection</span></span>

<span data-ttu-id="57378-142">En el directorio raíz del repositorio de hello, cree un archivo denominado *.env*.</span><span class="sxs-lookup"><span data-stu-id="57378-142">In hello repository root, create a file named *.env*.</span></span> <span data-ttu-id="57378-143">Hola copia siguiendo las variables en hello *.env* archivo.</span><span class="sxs-lookup"><span data-stu-id="57378-143">Copy hello following variables into hello *.env* file.</span></span> <span data-ttu-id="57378-144">Reemplace hello  _&lt;root_password >_ marcador de posición con la contraseña del usuario de hello MySQL raíz.</span><span class="sxs-lookup"><span data-stu-id="57378-144">Replace hello _&lt;root_password>_ placeholder with hello MySQL root user's password.</span></span>

```
APP_ENV=local
APP_DEBUG=true
APP_KEY=SomeRandomString

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_DATABASE=sampledb
DB_USERNAME=root
DB_PASSWORD=<root_password>
```

<span data-ttu-id="57378-145">Para obtener información acerca de cómo Laravel usa hello _.env_ de archivos, consulte [Laravel configuración de entorno](https://laravel.com/docs/5.4/configuration#environment-configuration).</span><span class="sxs-lookup"><span data-stu-id="57378-145">For information on how Laravel uses hello _.env_ file, see [Laravel Environment Configuration](https://laravel.com/docs/5.4/configuration#environment-configuration).</span></span>

### <a name="run-hello-sample-locally"></a><span data-ttu-id="57378-146">Ejecutar el ejemplo hello localmente</span><span class="sxs-lookup"><span data-stu-id="57378-146">Run hello sample locally</span></span>

<span data-ttu-id="57378-147">Ejecutar [migraciones de base de datos de Laravel](https://laravel.com/docs/5.4/migrations) toocreate Hola tablas hello las necesidades de aplicación.</span><span class="sxs-lookup"><span data-stu-id="57378-147">Run [Laravel database migrations](https://laravel.com/docs/5.4/migrations) toocreate hello tables hello application needs.</span></span> <span data-ttu-id="57378-148">toosee qué tablas se crean en las migraciones de hello, busque en hello _base de datos/migraciones_ directorio en el repositorio de Git Hola.</span><span class="sxs-lookup"><span data-stu-id="57378-148">toosee which tables are created in hello migrations, look in hello _database/migrations_ directory in hello Git repository.</span></span>

```bash
php artisan migrate
```

<span data-ttu-id="57378-149">Genere una nueva clave de aplicación Laravel.</span><span class="sxs-lookup"><span data-stu-id="57378-149">Generate a new Laravel application key.</span></span>

```bash
php artisan key:generate
```

<span data-ttu-id="57378-150">Ejecute la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="57378-150">Run hello application.</span></span>

```bash
php artisan serve
```

<span data-ttu-id="57378-151">Navegue demasiado`http://localhost:8000` en un explorador.</span><span class="sxs-lookup"><span data-stu-id="57378-151">Navigate too`http://localhost:8000` in a browser.</span></span> <span data-ttu-id="57378-152">Agregue algunas tareas en la página de Hola.</span><span class="sxs-lookup"><span data-stu-id="57378-152">Add a few tasks in hello page.</span></span>

![PHP conecta correctamente tooMySQL](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

<span data-ttu-id="57378-154">Escriba toostop PHP, `Ctrl + C` Hola terminal.</span><span class="sxs-lookup"><span data-stu-id="57378-154">toostop PHP, type `Ctrl + C` in hello terminal.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-mysql-in-azure"></a><span data-ttu-id="57378-155">Creación de MySQL en Azure</span><span class="sxs-lookup"><span data-stu-id="57378-155">Create MySQL in Azure</span></span>

<span data-ttu-id="57378-156">En este paso, creará una base de datos MySQL en [Azure Database for MySQL (versión preliminar)](/azure/mysql).</span><span class="sxs-lookup"><span data-stu-id="57378-156">In this step, you create a MySQL database in [Azure Database for MySQL (Preview)](/azure/mysql).</span></span> <span data-ttu-id="57378-157">Posteriormente, configurar base de datos de hello PHP aplicación tooconnect toothis.</span><span class="sxs-lookup"><span data-stu-id="57378-157">Later, you configure hello PHP application tooconnect toothis database.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="57378-158">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="57378-158">Create a resource group</span></span>

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group-no-h.md)] 

### <a name="create-a-mysql-server"></a><span data-ttu-id="57378-159">Creación de un servidor MySQL</span><span class="sxs-lookup"><span data-stu-id="57378-159">Create a MySQL server</span></span>

<span data-ttu-id="57378-160">Crear un servidor de base de datos de Azure para MySQL (versión preliminar) con hello [crear servidor de mysql az](/cli/azure/mysql/server#create) comando.</span><span class="sxs-lookup"><span data-stu-id="57378-160">Create a server in Azure Database for MySQL (Preview) with hello [az mysql server create](/cli/azure/mysql/server#create) command.</span></span>

<span data-ttu-id="57378-161">Hola siguiente comando, sustituya el nombre del servidor MySQL donde verá hello  _&lt;mysql_server_name >_ marcador de posición (los caracteres válidos son `a-z`, `0-9`, y `-`).</span><span class="sxs-lookup"><span data-stu-id="57378-161">In hello following command, substitute your MySQL server name where you see hello _&lt;mysql_server_name>_ placeholder (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="57378-162">Este nombre forma parte del nombre de host del servidor de MySQL de hello (`<mysql_server_name>.database.windows.net`), necesita toobe único global.</span><span class="sxs-lookup"><span data-stu-id="57378-162">This name is part of hello MySQL server's hostname  (`<mysql_server_name>.database.windows.net`), it needs toobe globally unique.</span></span>

```azurecli-interactive
az mysql server create \
    --name <mysql_server_name> \
    --resource-group myResourceGroup \
    --location "North Europe" \
    --admin-user adminuser \
    --admin-password MySQLAzure2017
```

<span data-ttu-id="57378-163">Cuando se crea el servidor de MySQL de hello, Hola CLI de Azure muestra información toohello similar siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="57378-163">When hello MySQL server is created, hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "administratorLogin": "adminuser",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "<mysql_server_name>.database.windows.net",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforMySQL/servers/<mysql_server_name>",
  "location": "northeurope",
  "name": "<mysql_server_name>",
  "resourceGroup": "myResourceGroup",
  ...
}
```

### <a name="configure-server-firewall"></a><span data-ttu-id="57378-164">Configuración del firewall del servidor</span><span class="sxs-lookup"><span data-stu-id="57378-164">Configure server firewall</span></span>

<span data-ttu-id="57378-165">Cree una regla de firewall para el cliente de MySQL server tooallow conexiones con hello [crear az mysql server regla de firewall](/cli/azure/mysql/server/firewall-rule#create) comando.</span><span class="sxs-lookup"><span data-stu-id="57378-165">Create a firewall rule for your MySQL server tooallow client connections by using hello [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create) command.</span></span>

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name> \
    --resource-group myResourceGroup \
    --start-ip-address 0.0.0.0 \
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="57378-166">Base de datos de Azure para MySQL (versión preliminar) actualmente no limita los servicios de tooAzure solo de las conexiones.</span><span class="sxs-lookup"><span data-stu-id="57378-166">Azure Database for MySQL (Preview) doesn't currently limit connections only tooAzure services.</span></span> <span data-ttu-id="57378-167">Tal y como se asignan dinámicamente direcciones IP en Azure, es mejor tooenable todas las direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="57378-167">As IP addresses in Azure are dynamically assigned, it is better tooenable all IP addresses.</span></span> <span data-ttu-id="57378-168">servicio de Hello está en vista previa.</span><span class="sxs-lookup"><span data-stu-id="57378-168">hello service is in preview.</span></span> <span data-ttu-id="57378-169">Se planean los mejores métodos para proteger la base de datos.</span><span class="sxs-lookup"><span data-stu-id="57378-169">Better methods for securing your database are planned.</span></span>
>
>

### <a name="connect-tooproduction-mysql-server-locally"></a><span data-ttu-id="57378-170">Conectar tooproduction MySQL server localmente</span><span class="sxs-lookup"><span data-stu-id="57378-170">Connect tooproduction MySQL server locally</span></span>

<span data-ttu-id="57378-171">En la ventana de terminal de hello, conectar toohello MySQL server en Azure.</span><span class="sxs-lookup"><span data-stu-id="57378-171">In hello terminal window, connect toohello MySQL server in Azure.</span></span> <span data-ttu-id="57378-172">Usar valor de Hola que especificó anteriormente por  _&lt;mysql_server_name >_.</span><span class="sxs-lookup"><span data-stu-id="57378-172">Use hello value you specified previously for _&lt;mysql_server_name>_.</span></span>

```bash
mysql -u adminuser@<mysql_server_name> -h <mysql_server_name>.database.windows.net -P 3306 -p
```

<span data-ttu-id="57378-173">Cuando se le pida una contraseña, utilice _tr0ngPa $$ w0rd!_, que especificó cuando creó la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="57378-173">When prompted for a password, use _$tr0ngPa$w0rd!_, which you specified when you created hello database.</span></span>

### <a name="create-a-production-database"></a><span data-ttu-id="57378-174">Creación de una base de datos de producción</span><span class="sxs-lookup"><span data-stu-id="57378-174">Create a production database</span></span>

<span data-ttu-id="57378-175">En hello `mysql` símbolo del sistema, cree una base de datos.</span><span class="sxs-lookup"><span data-stu-id="57378-175">At hello `mysql` prompt, create a database.</span></span>

```sql
CREATE DATABASE sampledb;
```

### <a name="create-a-user-with-permissions"></a><span data-ttu-id="57378-176">Creación de un usuario con permisos</span><span class="sxs-lookup"><span data-stu-id="57378-176">Create a user with permissions</span></span>

<span data-ttu-id="57378-177">Cree un usuario de base de datos llamado _phpappuser_ y conceder a todos los privilegios de hello `sampledb` base de datos.</span><span class="sxs-lookup"><span data-stu-id="57378-177">Create a database user called _phpappuser_ and give it all privileges in hello `sampledb` database.</span></span>

```sql
CREATE USER 'phpappuser' IDENTIFIED BY 'MySQLAzure2017'; 
GRANT ALL PRIVILEGES ON sampledb.* too'phpappuser';
```

<span data-ttu-id="57378-178">Salir de conexión del servidor de hello escribiendo `quit`.</span><span class="sxs-lookup"><span data-stu-id="57378-178">Exit hello server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="connect-app-tooazure-mysql"></a><span data-ttu-id="57378-179">Conectar aplicaciones tooAzure MySQL</span><span class="sxs-lookup"><span data-stu-id="57378-179">Connect app tooAzure MySQL</span></span>

<span data-ttu-id="57378-180">En este paso, se conectará Hola PHP aplicación toohello base de datos MySQL que creó en la base de datos de Azure para MySQL (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="57378-180">In this step, you connect hello PHP application toohello MySQL database you created in Azure Database for MySQL (Preview).</span></span>

<a name="devconfig"></a>

### <a name="configure-hello-database-connection"></a><span data-ttu-id="57378-181">Configurar conexión de base de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="57378-181">Configure hello database connection</span></span>

<span data-ttu-id="57378-182">En el directorio raíz del repositorio de hello, cree un _. env.production_ Hola de archivo y copie después de las variables en él.</span><span class="sxs-lookup"><span data-stu-id="57378-182">In hello repository root, create an _.env.production_ file and copy hello following variables into it.</span></span> <span data-ttu-id="57378-183">Reemplace el marcador de posición de hello  _&lt;mysql_server_name >_.</span><span class="sxs-lookup"><span data-stu-id="57378-183">Replace hello placeholder _&lt;mysql_server_name>_.</span></span>

```
APP_ENV=production
APP_DEBUG=true
APP_KEY=SomeRandomString

DB_CONNECTION=mysql
DB_HOST=<mysql_server_name>.database.windows.net
DB_DATABASE=sampledb
DB_USERNAME=phpappuser@<mysql_server_name>
DB_PASSWORD=MySQLAzure2017
MYSQL_SSL=true
```

<span data-ttu-id="57378-184">Guarde los cambios de Hola.</span><span class="sxs-lookup"><span data-stu-id="57378-184">Save hello changes.</span></span>

> [!TIP]
> <span data-ttu-id="57378-185">toosecure la información de conexión de MySQL, este archivo ya está excluida de repositorio de Git de hello (vea _.gitignore_ en el directorio raíz del repositorio hello).</span><span class="sxs-lookup"><span data-stu-id="57378-185">toosecure your MySQL connection information, this file is already excluded from hello Git repository (See _.gitignore_ in hello repository root).</span></span> <span data-ttu-id="57378-186">Más adelante, aprenderá cómo variables de entorno de tooconfigure de tooyour tooconnect de servicio de aplicaciones de base de datos en la base de datos de Azure para MySQL (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="57378-186">Later, you learn how tooconfigure environment variables in App Service tooconnect tooyour database in Azure Database for MySQL (Preview).</span></span> <span data-ttu-id="57378-187">Con las variables de entorno, no es necesario hello *.env* archivo en el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="57378-187">With environment variables, you don't need hello *.env* file in App Service.</span></span>
>

### <a name="configure-ssl-certificate"></a><span data-ttu-id="57378-188">Configuración de un certificado SSL</span><span class="sxs-lookup"><span data-stu-id="57378-188">Configure SSL certificate</span></span>

<span data-ttu-id="57378-189">De manera predeterminada, Azure Database for MySQL aplica las conexiones SSL de los clientes.</span><span class="sxs-lookup"><span data-stu-id="57378-189">By default, Azure Database for MySQL enforces SSL connections from clients.</span></span> <span data-ttu-id="57378-190">tooconnect tooyour base de datos MySQL en Azure, debe usar un _.pem_ certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="57378-190">tooconnect tooyour MySQL database in Azure, you must use a _.pem_ SSL certificate.</span></span>

<span data-ttu-id="57378-191">Abra _config/database.php_ y agregue hello _sslmode_ y _opciones_ parámetros demasiado`connections.mysql`, tal y como se muestra en el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="57378-191">Open _config/database.php_ and add hello _sslmode_ and _options_ parameters too`connections.mysql`, as shown in hello following code.</span></span>

```php
'mysql' => [
    ...
    'sslmode' => env('DB_SSLMODE', 'prefer'),
    'options' => (env('MYSQL_SSL')) ? [
        PDO::MYSQL_ATTR_SSL_KEY    => '/ssl/certificate.pem', 
    ] : []
],
```

<span data-ttu-id="57378-192">toolearn cómo toogenerate esto _certificate.pem_, consulte [tooAzure base de datos de conexión de conectividad de configurar SSL en su aplicación toosecurely para MySQL](../mysql/howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="57378-192">toolearn how toogenerate this _certificate.pem_, see [Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL](../mysql/howto-configure-ssl.md).</span></span>

> [!TIP]
> <span data-ttu-id="57378-193">ruta de acceso de Hello _/ssl/certificate.pem_ señala existente tooan _certificate.pem_ archivo en el repositorio de Git Hola.</span><span class="sxs-lookup"><span data-stu-id="57378-193">hello path _/ssl/certificate.pem_ points tooan existing _certificate.pem_ file in hello Git repository.</span></span> <span data-ttu-id="57378-194">Para su comodidad, en este tutorial se proporciona este archivo.</span><span class="sxs-lookup"><span data-stu-id="57378-194">This file is provided for convenience in this tutorial.</span></span> <span data-ttu-id="57378-195">Como procedimiento recomendado, no debe confirmar los certificados _.pem_ en el control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="57378-195">For best practice, you should not commit your _.pem_ certificates into source control.</span></span> 
>

### <a name="test-hello-application-locally"></a><span data-ttu-id="57378-196">Probar la aplicación hello localmente</span><span class="sxs-lookup"><span data-stu-id="57378-196">Test hello application locally</span></span>

<span data-ttu-id="57378-197">Ejecutar migraciones de base de datos de Laravel con _. env.production_ como Hola tablas de Hola de toocreate de archivos de entorno de la base de datos MySQL en la base de datos de Azure para MySQL (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="57378-197">Run Laravel database migrations with _.env.production_ as hello environment file toocreate hello tables in your MySQL database in Azure Database for MySQL (Preview).</span></span> <span data-ttu-id="57378-198">Recuerde que _. env.production_ tiene la base de datos MySQL tooyour de información de conexión de hello en Azure.</span><span class="sxs-lookup"><span data-stu-id="57378-198">Remember that _.env.production_ has hello connection information tooyour MySQL database in Azure.</span></span>

```bash
php artisan migrate --env=production --force
```

<span data-ttu-id="57378-199">El archivo _.env.production_ aún no cuenta con una clave de aplicación válida.</span><span class="sxs-lookup"><span data-stu-id="57378-199">_.env.production_ doesn't have a valid application key yet.</span></span> <span data-ttu-id="57378-200">Generar una nueva contraseña para él en hello terminal.</span><span class="sxs-lookup"><span data-stu-id="57378-200">Generate a new one for it in hello terminal.</span></span>

```bash
php artisan key:generate --env=production --force
```

<span data-ttu-id="57378-201">Ejecutar la aplicación de ejemplo Hola _. env.production_ como archivo de entorno de hello.</span><span class="sxs-lookup"><span data-stu-id="57378-201">Run hello sample application with _.env.production_ as hello environment file.</span></span>

```bash
php artisan serve --env=production
```

<span data-ttu-id="57378-202">Navegue demasiado`http://localhost:8000`.</span><span class="sxs-lookup"><span data-stu-id="57378-202">Navigate too`http://localhost:8000`.</span></span> <span data-ttu-id="57378-203">Si la página de Hola se carga sin errores, Hola aplicación PHP está conectando toohello base de datos MySQL en Azure.</span><span class="sxs-lookup"><span data-stu-id="57378-203">If hello page loads without errors, hello PHP application is connecting toohello MySQL database in Azure.</span></span>

<span data-ttu-id="57378-204">Agregue algunas tareas en la página de Hola.</span><span class="sxs-lookup"><span data-stu-id="57378-204">Add a few tasks in hello page.</span></span>

![PHP conecta correctamente tooAzure base de datos de MySQL (versión preliminar)](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

<span data-ttu-id="57378-206">Escriba toostop PHP, `Ctrl + C` Hola terminal.</span><span class="sxs-lookup"><span data-stu-id="57378-206">toostop PHP, type `Ctrl + C` in hello terminal.</span></span>

### <a name="commit-your-changes"></a><span data-ttu-id="57378-207">Confirmación de los cambios</span><span class="sxs-lookup"><span data-stu-id="57378-207">Commit your changes</span></span>

<span data-ttu-id="57378-208">Ejecute hello después toocommit de comandos de Git los cambios:</span><span class="sxs-lookup"><span data-stu-id="57378-208">Run hello following Git commands toocommit your changes:</span></span>

```bash
git add .
git commit -m "database.php updates"
```

<span data-ttu-id="57378-209">La aplicación es listo toobe implementado.</span><span class="sxs-lookup"><span data-stu-id="57378-209">Your app is ready toobe deployed.</span></span>

## <a name="deploy-tooazure"></a><span data-ttu-id="57378-210">Implementar tooAzure</span><span class="sxs-lookup"><span data-stu-id="57378-210">Deploy tooAzure</span></span>

<span data-ttu-id="57378-211">En este paso, implementará Hola conectado MySQL PHP aplicación tooAzure servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="57378-211">In this step, you deploy hello MySQL-connected PHP application tooAzure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="57378-212">Creación de un plan de App Service</span><span class="sxs-lookup"><span data-stu-id="57378-212">Create an App Service plan</span></span>

[!INCLUDE [Create app service plan no h](../../includes/app-service-web-create-app-service-plan-no-h.md)]

### <a name="create-a-web-app"></a><span data-ttu-id="57378-213">Creación de una aplicación web</span><span class="sxs-lookup"><span data-stu-id="57378-213">Create a web app</span></span>

[!INCLUDE [Create web app no h](../../includes/app-service-web-create-web-app-no-h.md)]

### <a name="set-hello-php-version"></a><span data-ttu-id="57378-214">Versión de PHP Hola de conjunto</span><span class="sxs-lookup"><span data-stu-id="57378-214">Set hello PHP version</span></span>

<span data-ttu-id="57378-215">Versión de PHP de Hola de conjunto que Hola aplicación requiere mediante hello [conjunto de configuración de aplicación Web de az](/cli/azure/webapp/config#set) comando.</span><span class="sxs-lookup"><span data-stu-id="57378-215">Set hello PHP version that hello application requires by using hello [az webapp config set](/cli/azure/webapp/config#set) command.</span></span>

<span data-ttu-id="57378-216">Hello siguiente comando establece Hola PHP versión too_7.0_.</span><span class="sxs-lookup"><span data-stu-id="57378-216">hello following command sets hello PHP version too_7.0_.</span></span>

```azurecli-interactive
az webapp config set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --php-version 7.0
```

### <a name="configure-database-settings"></a><span data-ttu-id="57378-217">Configuración de la base de datos</span><span class="sxs-lookup"><span data-stu-id="57378-217">Configure database settings</span></span>

<span data-ttu-id="57378-218">Como se indicó anteriormente, puede conectarse tooyour de base de datos de MySQL de Azure mediante variables de entorno de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="57378-218">As pointed out previously, you can connect tooyour Azure MySQL database using environment variables in App Service.</span></span>

<span data-ttu-id="57378-219">En el servicio de aplicación, establecer variables de entorno como _configuración de la aplicación_ mediante el uso de hello [az webapp configuración appsettings conjunto](/cli/azure/webapp/config/appsettings#set) comando.</span><span class="sxs-lookup"><span data-stu-id="57378-219">In App Service, you set environment variables as _app settings_ by using hello [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) command.</span></span>

<span data-ttu-id="57378-220">Hello siguiente comando configura configuración de la aplicación hello `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, y `DB_PASSWORD`.</span><span class="sxs-lookup"><span data-stu-id="57378-220">hello following command configures hello app settings `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, and `DB_PASSWORD`.</span></span> <span data-ttu-id="57378-221">Reemplace los marcadores de posición de hello  _&lt;appname >_ y  _&lt;mysql_server_name >_.</span><span class="sxs-lookup"><span data-stu-id="57378-221">Replace hello placeholders _&lt;appname>_ and _&lt;mysql_server_name>_.</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings DB_HOST="<mysql_server_name>.database.windows.net" DB_DATABASE="sampledb" DB_USERNAME="phpappuser@<mysql_server_name>" DB_PASSWORD="MySQLAzure2017" MYSQL_SSL="true"
```

<span data-ttu-id="57378-222">Puede usar hello PHP [getenv](http://www.php.net/manual/function.getenv.php) método tooaccess Hola configuración.</span><span class="sxs-lookup"><span data-stu-id="57378-222">You can use hello PHP [getenv](http://www.php.net/manual/function.getenv.php) method tooaccess hello settings.</span></span> <span data-ttu-id="57378-223">Hola Laravel código usa un [env](https://laravel.com/docs/5.4/helpers#method-env) contenedor a través de hello PHP `getenv`.</span><span class="sxs-lookup"><span data-stu-id="57378-223">hello Laravel code uses an [env](https://laravel.com/docs/5.4/helpers#method-env) wrapper over hello PHP `getenv`.</span></span> <span data-ttu-id="57378-224">Por ejemplo, configuración de MySQL de hello en _config/database.php_ aspecto Hola siguiente código:</span><span class="sxs-lookup"><span data-stu-id="57378-224">For example, hello MySQL configuration in _config/database.php_ looks like hello following code:</span></span>

```php
'mysql' => [
    'driver'    => 'mysql',
    'host'      => env('DB_HOST', 'localhost'),
    'database'  => env('DB_DATABASE', 'forge'),
    'username'  => env('DB_USERNAME', 'forge'),
    'password'  => env('DB_PASSWORD', ''),
    ...
],
```

### <a name="configure-laravel-environment-variables"></a><span data-ttu-id="57378-225">Configuración de las variables de entorno de Laravel</span><span class="sxs-lookup"><span data-stu-id="57378-225">Configure Laravel environment variables</span></span>

<span data-ttu-id="57378-226">Laravel necesita una clave de aplicación en App Service.</span><span class="sxs-lookup"><span data-stu-id="57378-226">Laravel needs an application key in App Service.</span></span> <span data-ttu-id="57378-227">Puede configurarlo con valores de aplicación.</span><span class="sxs-lookup"><span data-stu-id="57378-227">You can configure it with app settings.</span></span>

<span data-ttu-id="57378-228">Use `php artisan` toogenerate una nueva clave de aplicación sin guardarlo too_.env_.</span><span class="sxs-lookup"><span data-stu-id="57378-228">Use `php artisan` toogenerate a new application key without saving it too_.env_.</span></span>

```bash
php artisan key:generate --show
```

<span data-ttu-id="57378-229">Establecer tecla de aplicación Hola Hola servicio de aplicaciones de aplicación web mediante hello [az webapp configuración appsettings conjunto](/cli/azure/webapp/config/appsettings#set) comando.</span><span class="sxs-lookup"><span data-stu-id="57378-229">Set hello application key in hello App Service web app by using hello [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) command.</span></span> <span data-ttu-id="57378-230">Reemplace los marcadores de posición de hello  _&lt;appname >_ y  _&lt;outputofphpartisankey: generar >_.</span><span class="sxs-lookup"><span data-stu-id="57378-230">Replace hello placeholders _&lt;appname>_ and _&lt;outputofphpartisankey:generate>_.</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings APP_KEY="<output_of_php_artisan_key:generate>" APP_DEBUG="true"
```

<span data-ttu-id="57378-231">`APP_DEBUG="true"`indica Laravel tooreturn información de depuración cuando Hola implementa la aplicación web encuentra errores.</span><span class="sxs-lookup"><span data-stu-id="57378-231">`APP_DEBUG="true"` tells Laravel tooreturn debugging information when hello deployed web app encounters errors.</span></span> <span data-ttu-id="57378-232">Al ejecutar una aplicación de producción, se establece demasiado`false`, que es más seguro.</span><span class="sxs-lookup"><span data-stu-id="57378-232">When running a production application, set it too`false`, which is more secure.</span></span>

### <a name="set-hello-virtual-application-path"></a><span data-ttu-id="57378-233">Establecer la ruta de aplicación virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="57378-233">Set hello virtual application path</span></span>

<span data-ttu-id="57378-234">Establecer ruta de acceso de aplicación virtual de hello para la aplicación web de Hola.</span><span class="sxs-lookup"><span data-stu-id="57378-234">Set hello virtual application path for hello web app.</span></span> <span data-ttu-id="57378-235">Este paso es necesario porque hello [ciclo de vida de aplicación Laravel](https://laravel.com/docs/5.4/lifecycle) comienza en hello _público_ directorio en lugar del directorio raíz de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="57378-235">This step is required because hello [Laravel application lifecycle](https://laravel.com/docs/5.4/lifecycle) begins in hello _public_ directory instead of hello application's root directory.</span></span> <span data-ttu-id="57378-236">Otros marcos PHP cuyo ciclo de vida de inicio en el directorio raíz de hello pueden trabajar sin necesidad de configuración manual de hello ruta de acceso virtual.</span><span class="sxs-lookup"><span data-stu-id="57378-236">Other PHP frameworks whose lifecycle start in hello root directory can work without manual configuration of hello virtual application path.</span></span>

<span data-ttu-id="57378-237">Establecer la ruta de aplicación virtual de hello mediante el uso de hello [actualización de recursos az](/cli/azure/resource#update) comando.</span><span class="sxs-lookup"><span data-stu-id="57378-237">Set hello virtual application path by using hello [az resource update](/cli/azure/resource#update) command.</span></span> <span data-ttu-id="57378-238">Reemplace hello  _&lt;appname >_ marcador de posición.</span><span class="sxs-lookup"><span data-stu-id="57378-238">Replace hello _&lt;appname>_ placeholder.</span></span>

```azurecli-interactive
az resource update \
    --name web \
    --resource-group myResourceGroup \
    --namespace Microsoft.Web \
    --resource-type config \
    --parent sites/<app_name> \
    --set properties.virtualApplications[0].physicalPath="site\wwwroot\public" \
    --api-version 2015-06-01
```

<span data-ttu-id="57378-239">De forma predeterminada, el servicio de aplicación de Azure puntos de ruta de acceso de aplicación virtual de raíz de hello (_/_) directorio de raíz de toohello de hello implementa archivos de aplicación (_sites\wwwroot_).</span><span class="sxs-lookup"><span data-stu-id="57378-239">By default, Azure App Service points hello root virtual application path (_/_) toohello root directory of hello deployed application files (_sites\wwwroot_).</span></span>

### <a name="configure-a-deployment-user"></a><span data-ttu-id="57378-240">Configuración de un usuario de implementación</span><span class="sxs-lookup"><span data-stu-id="57378-240">Configure a deployment user</span></span>

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user-no-h.md)]

### <a name="configure-local-git-deployment"></a><span data-ttu-id="57378-241">Configurar la implementación de Git local</span><span class="sxs-lookup"><span data-stu-id="57378-241">Configure local Git deployment</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git-no-h.md)]

### <a name="push-tooazure-from-git"></a><span data-ttu-id="57378-242">TooAzure de inserción de Git</span><span class="sxs-lookup"><span data-stu-id="57378-242">Push tooAzure from Git</span></span>

<span data-ttu-id="57378-243">Agregue un repositorio de Git local de Azure tooyour remoto.</span><span class="sxs-lookup"><span data-stu-id="57378-243">Add an Azure remote tooyour local Git repository.</span></span>

```bash
git remote add azure <paste_copied_url_here>
```

<span data-ttu-id="57378-244">Insertar la aplicación PHP de toohello toodeploy remoto Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="57378-244">Push toohello Azure remote toodeploy hello PHP application.</span></span> <span data-ttu-id="57378-245">Se le solicite para contraseña de Hola que proporcionó anteriormente como parte de la creación de hello de usuario de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="57378-245">You are prompted for hello password you supplied earlier as part of hello creation of hello deployment user.</span></span>

```bash
git push azure master
```

<span data-ttu-id="57378-246">Durante la implementación, Azure App Service comunicará su progreso con Git.</span><span class="sxs-lookup"><span data-stu-id="57378-246">During deployment, Azure App Service communicates its progress with Git.</span></span>

```bash
Counting objects: 3, done.
Delta compression using up too8 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 291 bytes | 0 bytes/s, done.
Total 3 (delta 2), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'a5e076db9c'.
remote: Running custom deployment command...
remote: Running deployment command...
...
< Output has been truncated for readability >
```

> [!NOTE]
> <span data-ttu-id="57378-247">Puede observar que el proceso de implementación de hello instala [compositor](https://getcomposer.org/) paquetes final Hola.</span><span class="sxs-lookup"><span data-stu-id="57378-247">You may notice that hello deployment process installs [Composer](https://getcomposer.org/) packages at hello end.</span></span> <span data-ttu-id="57378-248">Servicio de aplicaciones no ejecuta estos automatizaciones durante la implementación de forma predeterminada, por lo que este repositorio de ejemplo tiene tres adicionales archivos en su tooenable del directorio raíz que:</span><span class="sxs-lookup"><span data-stu-id="57378-248">App Service does not run these automations during default deployment, so this sample repository has three additional files in its root directory tooenable it:</span></span>
>
> - <span data-ttu-id="57378-249">`.deployment`-Este archivo indica toorun de servicio de aplicaciones `bash deploy.sh` como script de implementación personalizada de Hola.</span><span class="sxs-lookup"><span data-stu-id="57378-249">`.deployment` - This file tells App Service toorun `bash deploy.sh` as hello custom deployment script.</span></span>
> - <span data-ttu-id="57378-250">`deploy.sh`-Hola script de implementación personalizado.</span><span class="sxs-lookup"><span data-stu-id="57378-250">`deploy.sh` - hello custom deployment script.</span></span> <span data-ttu-id="57378-251">Si examina el archivo hello, verá que se ejecuta `php composer.phar install` después `npm install`.</span><span class="sxs-lookup"><span data-stu-id="57378-251">If you review hello file, you will see that it runs `php composer.phar install` after `npm install`.</span></span>
> - <span data-ttu-id="57378-252">`composer.phar`-Administrador de paquetes de saludo compositor.</span><span class="sxs-lookup"><span data-stu-id="57378-252">`composer.phar` - hello Composer package manager.</span></span>
>
> <span data-ttu-id="57378-253">Puede usar este enfoque tooadd cualquier tooApp de implementación basado en Git tooyour paso servicio.</span><span class="sxs-lookup"><span data-stu-id="57378-253">You can use this approach tooadd any step tooyour Git-based deployment tooApp Service.</span></span> <span data-ttu-id="57378-254">Para obtener más información, consulte [Custom Deployment Script](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script) (Script de implementación personalizado).</span><span class="sxs-lookup"><span data-stu-id="57378-254">For more information, see [Custom Deployment Script](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script).</span></span>
>

### <a name="browse-toohello-azure-web-app"></a><span data-ttu-id="57378-255">Examinar la aplicación web de Azure de toohello</span><span class="sxs-lookup"><span data-stu-id="57378-255">Browse toohello Azure web app</span></span>

<span data-ttu-id="57378-256">Examinar demasiado`http://<app_name>.azurewebsites.net` y agregar algunas tareas toohello lista.</span><span class="sxs-lookup"><span data-stu-id="57378-256">Browse too`http://<app_name>.azurewebsites.net` and add a few tasks toohello list.</span></span>

![Aplicación PHP que se ejecuta en Azure App Service](./media/app-service-web-tutorial-php-mysql/php-mysql-in-azure.png)

<span data-ttu-id="57378-258">Ya está ejecutando una aplicación PHP orientada a datos en Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="57378-258">Congratulations, you're running a data-driven PHP app in Azure App Service.</span></span>

## <a name="update-model-locally-and-redeploy"></a><span data-ttu-id="57378-259">Actualización local del modelo y nueva implementación</span><span class="sxs-lookup"><span data-stu-id="57378-259">Update model locally and redeploy</span></span>

<span data-ttu-id="57378-260">En este paso, realice un cambio sencillo toohello `task` datos de modelo y Hola webapp y, a continuación, publicar Hola actualización tooAzure.</span><span class="sxs-lookup"><span data-stu-id="57378-260">In this step, you make a simple change toohello `task` data model and hello webapp, and then publish hello update tooAzure.</span></span>

<span data-ttu-id="57378-261">Para el escenario de tareas de hello, modificar aplicación hello por lo que puede marcar una tarea como completa.</span><span class="sxs-lookup"><span data-stu-id="57378-261">For hello tasks scenario, you modify hello application so that you can mark a task as complete.</span></span>

### <a name="add-a-column"></a><span data-ttu-id="57378-262">Adición de una columna</span><span class="sxs-lookup"><span data-stu-id="57378-262">Add a column</span></span>

<span data-ttu-id="57378-263">Hola terminal, vaya toohello raíz del repositorio de Git Hola.</span><span class="sxs-lookup"><span data-stu-id="57378-263">In hello terminal, navigate toohello root of hello Git repository.</span></span>

<span data-ttu-id="57378-264">Generar una migración de base de datos nueva para hello `tasks` tabla:</span><span class="sxs-lookup"><span data-stu-id="57378-264">Generate a new database migration for hello `tasks` table:</span></span>

```bash
php artisan make:migration add_complete_column --table=tasks
```

<span data-ttu-id="57378-265">Este comando mostrará Hola nombre del archivo de migración de Hola que se genera.</span><span class="sxs-lookup"><span data-stu-id="57378-265">This command shows you hello name of hello migration file that's generated.</span></span> <span data-ttu-id="57378-266">Busque este archivo en _database/migrations_ y ábralo.</span><span class="sxs-lookup"><span data-stu-id="57378-266">Find this file in _database/migrations_ and open it.</span></span>

<span data-ttu-id="57378-267">Reemplace hello `up` método con el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="57378-267">Replace hello `up` method with hello following code:</span></span>

```php
public function up()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->boolean('complete')->default(False);
    });
}
```

<span data-ttu-id="57378-268">Hello código anterior agrega una columna booleana en hello `tasks` tabla denominada `complete`.</span><span class="sxs-lookup"><span data-stu-id="57378-268">hello preceding code adds a boolean column in hello `tasks` table called `complete`.</span></span>

<span data-ttu-id="57378-269">Reemplace hello `down` método con hello siguiente código para la acción de reversión de hello:</span><span class="sxs-lookup"><span data-stu-id="57378-269">Replace hello `down` method with hello following code for hello rollback action:</span></span>

```php
public function down()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->dropColumn('complete');
    });
}
```

<span data-ttu-id="57378-270">Hola terminal, ejecute las migraciones de base de datos de Laravel toomake cambios de hello en la base de datos local de Hola.</span><span class="sxs-lookup"><span data-stu-id="57378-270">In hello terminal, run Laravel database migrations toomake hello change in hello local database.</span></span>

```bash
php artisan migrate
```

<span data-ttu-id="57378-271">En función de hello [convención de nomenclatura de Laravel](https://laravel.com/docs/5.4/eloquent#defining-models), modelo de hello `Task` (vea _app/Task.php_) asigna toohello `tasks` tabla de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="57378-271">Based on hello [Laravel naming convention](https://laravel.com/docs/5.4/eloquent#defining-models), hello model `Task` (see _app/Task.php_) maps toohello `tasks` table by default.</span></span>

### <a name="update-application-logic"></a><span data-ttu-id="57378-272">Actualización de la lógica de aplicación</span><span class="sxs-lookup"><span data-stu-id="57378-272">Update application logic</span></span>

<span data-ttu-id="57378-273">Abra hello *routes/web.php* archivo.</span><span class="sxs-lookup"><span data-stu-id="57378-273">Open hello *routes/web.php* file.</span></span> <span data-ttu-id="57378-274">aplicación Hello define sus rutas y aquí la lógica de negocios.</span><span class="sxs-lookup"><span data-stu-id="57378-274">hello application defines its routes and business logic here.</span></span>

<span data-ttu-id="57378-275">Al final de Hola de archivo hello, agregue una ruta con hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="57378-275">At hello end of hello file, add a route with hello following code:</span></span>

```php
/**
 * Toggle Task completeness
 */
Route::post('/task/{id}', function ($id) {
    error_log('INFO: post /task/'.$id);
    $task = Task::findOrFail($id);

    $task->complete = !$task->complete;
    $task->save();

    return redirect('/');
});
```

<span data-ttu-id="57378-276">Hello código precedente crea un modelo de datos de una sencilla actualización toohello, cambie el valor de Hola de `complete`.</span><span class="sxs-lookup"><span data-stu-id="57378-276">hello preceding code makes a simple update toohello data model by toggling hello value of `complete`.</span></span>

### <a name="update-hello-view"></a><span data-ttu-id="57378-277">Actualizar vista Hola</span><span class="sxs-lookup"><span data-stu-id="57378-277">Update hello view</span></span>

<span data-ttu-id="57378-278">Abra hello *resources/views/tasks.blade.php* archivo.</span><span class="sxs-lookup"><span data-stu-id="57378-278">Open hello *resources/views/tasks.blade.php* file.</span></span> <span data-ttu-id="57378-279">Buscar hello `<tr>` etiqueta de apertura y reemplácela con:</span><span class="sxs-lookup"><span data-stu-id="57378-279">Find hello `<tr>` opening tag and replace it with:</span></span>

```html
<tr class="{{ $task->complete ? 'success' : 'active' }}" >
```

<span data-ttu-id="57378-280">Hola anterior cambia de color fila código Hola dependiendo de si la tarea hello es completa.</span><span class="sxs-lookup"><span data-stu-id="57378-280">hello preceding code changes hello row color depending on whether hello task is complete.</span></span>

<span data-ttu-id="57378-281">En la siguiente línea hello, deberá Hola siguiente código:</span><span class="sxs-lookup"><span data-stu-id="57378-281">In hello next line, you have hello following code:</span></span>

```html
<td class="table-text"><div>{{ $task->name }}</div></td>
```

<span data-ttu-id="57378-282">Reemplace toda la línea hello con hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="57378-282">Replace hello entire line with hello following code:</span></span>

```html
<td>
    <form action="{{ url('task/'.$task->id) }}" method="POST">
        {{ csrf_field() }}

        <button type="submit" class="btn btn-xs">
            <i class="fa {{$task->complete ? 'fa-check-square-o' : 'fa-square-o'}}"></i>
        </button>
        {{ $task->name }}
    </form>
</td>
```

<span data-ttu-id="57378-283">Hello código anterior agrega botón de envío de Hola que hace referencia la ruta de Hola que definió anteriormente.</span><span class="sxs-lookup"><span data-stu-id="57378-283">hello preceding code adds hello submit button that references hello route that you defined earlier.</span></span>

### <a name="test-hello-changes-locally"></a><span data-ttu-id="57378-284">Probar los cambios de hello localmente</span><span class="sxs-lookup"><span data-stu-id="57378-284">Test hello changes locally</span></span>

<span data-ttu-id="57378-285">Directorio raíz de hello del repositorio de Git de hello, ejecutar el servidor de desarrollo de Hola.</span><span class="sxs-lookup"><span data-stu-id="57378-285">From hello root directory of hello Git repository, run hello development server.</span></span>

```bash
php artisan serve
```

<span data-ttu-id="57378-286">Hola toosee cambio de estado de tareas, navegue demasiado`http://localhost:8000` y seleccione Hola casilla.</span><span class="sxs-lookup"><span data-stu-id="57378-286">toosee hello task status change, navigate too`http://localhost:8000` and select hello checkbox.</span></span>

![Casilla de verificación agregado tootask](./media/app-service-web-tutorial-php-mysql/complete-checkbox.png)

<span data-ttu-id="57378-288">Escriba toostop PHP, `Ctrl + C` Hola terminal.</span><span class="sxs-lookup"><span data-stu-id="57378-288">toostop PHP, type `Ctrl + C` in hello terminal.</span></span>

### <a name="publish-changes-tooazure"></a><span data-ttu-id="57378-289">Publicar cambios tooAzure</span><span class="sxs-lookup"><span data-stu-id="57378-289">Publish changes tooAzure</span></span>

<span data-ttu-id="57378-290">Hola terminal, ejecutar migraciones de base de datos de Laravel con cambio Hola producción conexión cadena toomake Hola Hola base de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="57378-290">In hello terminal, run Laravel database migrations with hello production connection string toomake hello change in hello Azure database.</span></span>

```bash
php artisan migrate --env=production --force
```

<span data-ttu-id="57378-291">Confirmar todos los cambios de hello en Git y, a continuación, insertar tooAzure de cambios de código de hello.</span><span class="sxs-lookup"><span data-stu-id="57378-291">Commit all hello changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git add .
git commit -m "added complete checkbox"
git push azure master
```

<span data-ttu-id="57378-292">Una vez Hola `git push` es completar, navegue toohello Azure web app y prueba Hola nueva funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="57378-292">Once hello `git push` is complete, navigate toohello Azure web app and test hello new functionality.</span></span>

![TooAzure publiquen los cambios de modelo y la base de datos](media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

<span data-ttu-id="57378-294">Si ha agregado las tareas, sí se conservan en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="57378-294">If you added any tasks, they are retained in hello database.</span></span> <span data-ttu-id="57378-295">Esquema de datos de las actualizaciones toohello dejar intacta la datos existentes.</span><span class="sxs-lookup"><span data-stu-id="57378-295">Updates toohello data schema leave existing data intact.</span></span>

## <a name="stream-diagnostic-logs"></a><span data-ttu-id="57378-296">Transmisión de registros de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="57378-296">Stream diagnostic logs</span></span>

<span data-ttu-id="57378-297">Mientras Hola aplicación PHP se ejecuta en el servicio de aplicación de Azure, puede obtener registros de consola hello tooyour canalizada terminal.</span><span class="sxs-lookup"><span data-stu-id="57378-297">While hello PHP application runs in Azure App Service, you can get hello console logs piped tooyour terminal.</span></span> <span data-ttu-id="57378-298">De este modo, puede obtener Hola mensajes de diagnóstico del mismo toohelp depurar errores de aplicación.</span><span class="sxs-lookup"><span data-stu-id="57378-298">That way, you can get hello same diagnostic messages toohelp you debug application errors.</span></span>

<span data-ttu-id="57378-299">registro toostart transmisión por secuencias, utilice hello [final del registro de aplicación Web az](/cli/azure/webapp/log#tail) comando.</span><span class="sxs-lookup"><span data-stu-id="57378-299">toostart log streaming, use hello [az webapp log tail](/cli/azure/webapp/log#tail) command.</span></span>

```azurecli-interactive
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup
```

<span data-ttu-id="57378-300">Cuando se inicia la transmisión por secuencias de registro, actualización de aplicación web de Azure de hello en hello explorador tooget cierto tráfico web.</span><span class="sxs-lookup"><span data-stu-id="57378-300">Once log streaming has started, refresh hello Azure web app in hello browser tooget some web traffic.</span></span> <span data-ttu-id="57378-301">Ahora puede ver terminal de toohello canalizada de registros de consola.</span><span class="sxs-lookup"><span data-stu-id="57378-301">You can now see console logs piped toohello terminal.</span></span> <span data-ttu-id="57378-302">Si no ve los registros de la consola de inmediato, vuelve a comprobarlo en 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="57378-302">If you don't see console logs immediately, check again in 30 seconds.</span></span>

<span data-ttu-id="57378-303">registro de toostop de transmisión por secuencias en cualquier momento, tipo `Ctrl` + `C`.</span><span class="sxs-lookup"><span data-stu-id="57378-303">toostop log streaming at anytime, type `Ctrl`+`C`.</span></span>

> [!TIP]
> <span data-ttu-id="57378-304">Una aplicación PHP puede usar el estándar de hello [error_log()](http://php.net/manual/function.error-log.php) toooutput toohello consola.</span><span class="sxs-lookup"><span data-stu-id="57378-304">A PHP application can use hello standard [error_log()](http://php.net/manual/function.error-log.php) toooutput toohello console.</span></span> <span data-ttu-id="57378-305">aplicación de ejemplo de Hola usa este enfoque en _app/Http/routes.php_.</span><span class="sxs-lookup"><span data-stu-id="57378-305">hello sample application uses this approach in _app/Http/routes.php_.</span></span>
>
> <span data-ttu-id="57378-306">Un marco de trabajo web, [Laravel utiliza Monolog](https://laravel.com/docs/5.4/errors) como proveedor de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="57378-306">As a web framework, [Laravel uses Monolog](https://laravel.com/docs/5.4/errors) as hello logging provider.</span></span> <span data-ttu-id="57378-307">toosee cómo tooget Monolog toooutput mensajes toohello consola, consulte [PHP: cómo toouse monolog toolog tooconsole (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out).</span><span class="sxs-lookup"><span data-stu-id="57378-307">toosee how tooget Monolog toooutput messages toohello console, see [PHP: How toouse monolog toolog tooconsole (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out).</span></span>
>
>

## <a name="manage-hello-azure-web-app"></a><span data-ttu-id="57378-308">Administrar la aplicación web de Azure de hello</span><span class="sxs-lookup"><span data-stu-id="57378-308">Manage hello Azure web app</span></span>

<span data-ttu-id="57378-309">Vaya toohello [portal de Azure](https://portal.azure.com) toomanage hello web aplicación que creó.</span><span class="sxs-lookup"><span data-stu-id="57378-309">Go toohello [Azure portal](https://portal.azure.com) toomanage hello web app you created.</span></span>

<span data-ttu-id="57378-310">Hola menú izquierdo, haga clic en **servicios de aplicaciones**y, a continuación, haga clic en nombre de saludo de la aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="57378-310">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Aplicación de navegación del portal tooAzure web](./media/app-service-web-tutorial-php-mysql/access-portal.png)

<span data-ttu-id="57378-312">Podrá ver la página de información general de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="57378-312">You see your web app's Overview page.</span></span> <span data-ttu-id="57378-313">Aquí se pueden realizar tareas de administración básicas como detener, iniciar, reiniciar, examinar y eliminar.</span><span class="sxs-lookup"><span data-stu-id="57378-313">Here, you can perform basic management tasks like  stop, start, restart, browse, and delete.</span></span>

<span data-ttu-id="57378-314">menú de la izquierda Hola proporciona páginas para la configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="57378-314">hello left menu provides pages for configuring your app.</span></span>

![Página de App Service en Azure Portal](./media/app-service-web-tutorial-php-mysql/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="57378-316">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="57378-316">Next steps</span></span>

<span data-ttu-id="57378-317">En este tutorial, aprendió a:</span><span class="sxs-lookup"><span data-stu-id="57378-317">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="57378-318">Crear una base de datos MySQL en Azure</span><span class="sxs-lookup"><span data-stu-id="57378-318">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="57378-319">Conectar un tooMySQL de aplicación PHP</span><span class="sxs-lookup"><span data-stu-id="57378-319">Connect a PHP app tooMySQL</span></span>
> * <span data-ttu-id="57378-320">Implementar Hola aplicación tooAzure</span><span class="sxs-lookup"><span data-stu-id="57378-320">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="57378-321">Actualizar el modelo de datos de Hola y volver a implementar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="57378-321">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="57378-322">Transmitir registros de diagnóstico desde Azure</span><span class="sxs-lookup"><span data-stu-id="57378-322">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="57378-323">Administrar aplicación Hola Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="57378-323">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="57378-324">Avanzar toohello siguiente tutorial toolearn cómo toomap un DNS personalizado nombre tooa web app.</span><span class="sxs-lookup"><span data-stu-id="57378-324">Advance toohello next tutorial toolearn how toomap a custom DNS name tooa web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="57378-325">Asignar un tooAzure de nombre DNS personalizado existente aplicaciones Web</span><span class="sxs-lookup"><span data-stu-id="57378-325">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
