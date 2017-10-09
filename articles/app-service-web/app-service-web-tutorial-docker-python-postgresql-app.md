---
title: "aaaBuild una aplicación web de Python de Docker y PostgreSQL en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo una aplicación de Python Docker tooget trabajando en Azure, con conexión tooa PostgreSQL base de datos."
services: app-service\web
documentationcenter: python
author: berndverst
manager: erikre
editor: 
ms.assetid: 2bada123-ef18-44e5-be71-e16323b20466
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: tutorial
ms.date: 05/03/2017
ms.author: beverst
ms.custom: mvc
ms.openlocfilehash: e594ef9ec8c04ef2bf725e5f998691f3fb8cf815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-docker-python-and-postgresql-web-app-in-azure"></a><span data-ttu-id="3167a-103">Compilación de una aplicación web Docker Python con PostgreSQL en Azure</span><span class="sxs-lookup"><span data-stu-id="3167a-103">Build a Docker Python and PostgreSQL web app in Azure</span></span>

<span data-ttu-id="3167a-104">Azure Web Apps proporciona un servicio de hospedaje web muy escalable y con aplicación de revisiones de un modo automático.</span><span class="sxs-lookup"><span data-stu-id="3167a-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="3167a-105">Este tutorial muestra cómo toocreate un Docker de Python básico web aplicación en Azure.</span><span class="sxs-lookup"><span data-stu-id="3167a-105">This tutorial shows how toocreate a basic Docker Python web app in Azure.</span></span> <span data-ttu-id="3167a-106">Se conectará a esta base de datos de aplicación tooa PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="3167a-106">You'll connect this app tooa PostgreSQL database.</span></span> <span data-ttu-id="3167a-107">Cuando haya terminado, tendrá una aplicación Python Flask que se ejecuta en un contenedor Docker en [Azure App Service Web Apps](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3167a-107">When you're done, you'll have a Python Flask application running within a Docker container on [Azure App Service Web Apps](app-service-web-overview.md).</span></span>

![Aplicación Docker Python Flask en Azure App Service](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

<span data-ttu-id="3167a-109">Puede seguir estos pasos hello en macOS.</span><span class="sxs-lookup"><span data-stu-id="3167a-109">You can follow hello steps below on macOS.</span></span> <span data-ttu-id="3167a-110">Instrucciones de Linux y Windows son Hola igual en la mayoría de los casos, pero no se detallan las diferencias de hello en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="3167a-110">Linux and Windows instructions are hello same in most cases, but hello differences are not detailed in this tutorial.</span></span>
 
## <a name="prerequisites"></a><span data-ttu-id="3167a-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3167a-111">Prerequisites</span></span>

<span data-ttu-id="3167a-112">toocomplete este tutorial:</span><span class="sxs-lookup"><span data-stu-id="3167a-112">toocomplete this tutorial:</span></span>

1. [<span data-ttu-id="3167a-113">Instalación de Git</span><span class="sxs-lookup"><span data-stu-id="3167a-113">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="3167a-114">Instalación de Python</span><span class="sxs-lookup"><span data-stu-id="3167a-114">Install Python</span></span>](https://www.python.org/downloads/)
1. [<span data-ttu-id="3167a-115">Instalación y ejecución de PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="3167a-115">Install and run PostgreSQL</span></span>](https://www.postgresql.org/download/)
1. [<span data-ttu-id="3167a-116">Instalación de Docker Community Edition</span><span class="sxs-lookup"><span data-stu-id="3167a-116">Install Docker Community Edition</span></span>](https://www.docker.com/community-edition)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="3167a-117">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="3167a-117">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="3167a-118">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="3167a-118">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="3167a-119">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3167a-119">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="test-local-postgresql-installation-and-create-a-database"></a><span data-ttu-id="3167a-120">Prueba de la instalación local de PostgreSQL y creación de una base de datos</span><span class="sxs-lookup"><span data-stu-id="3167a-120">Test local PostgreSQL installation and create a database</span></span>

<span data-ttu-id="3167a-121">Abra la ventana de terminal de Hola y ejecute `psql postgres` tooconnect tooyour servidor local de PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="3167a-121">Open hello terminal window and run `psql postgres` tooconnect tooyour local PostgreSQL server.</span></span>

```bash
psql postgres
```

<span data-ttu-id="3167a-122">Si la conexión se realiza correctamente, significa que la base de datos PostgreSQL está en ejecución.</span><span class="sxs-lookup"><span data-stu-id="3167a-122">If your connection is successful, your PostgreSQL database is running.</span></span> <span data-ttu-id="3167a-123">Si no es así, asegúrese de que se ha iniciado la base de datos PostgresQL local siguiendo los pasos de hello en [descargas - PostgreSQL Core distribución](https://www.postgresql.org/download/).</span><span class="sxs-lookup"><span data-stu-id="3167a-123">If not, make sure that your local PostgresQL database is started by following hello steps at [Downloads - PostgreSQL Core Distribution](https://www.postgresql.org/download/).</span></span>

<span data-ttu-id="3167a-124">Cree una base de datos denominada *eventregistration* y configure un usuario de base de datos independiente denominado *manager* cuya contraseña será *supersecretpass*.</span><span class="sxs-lookup"><span data-stu-id="3167a-124">Create a database called *eventregistration* and set up a separate database user named *manager* with password *supersecretpass*.</span></span>

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration toomanager;
```
<span data-ttu-id="3167a-125">Tipo de *\q* cliente de tooexit Hola PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="3167a-125">Type *\q* tooexit hello PostgreSQL client.</span></span> 

<a name="step2"></a>

## <a name="create-local-python-flask-application"></a><span data-ttu-id="3167a-126">Creación de una aplicación Python Flask local</span><span class="sxs-lookup"><span data-stu-id="3167a-126">Create local Python Flask application</span></span>

<span data-ttu-id="3167a-127">En este paso, configurar un proyecto Python matraz Hola local.</span><span class="sxs-lookup"><span data-stu-id="3167a-127">In this step, you set up hello local Python Flask project.</span></span>

### <a name="clone-hello-sample-application"></a><span data-ttu-id="3167a-128">Clonar aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="3167a-128">Clone hello sample application</span></span>

<span data-ttu-id="3167a-129">Ventana de terminal de hello abierto, y `CD` tooa directorio de trabajo.</span><span class="sxs-lookup"><span data-stu-id="3167a-129">Open hello terminal window, and `CD` tooa working directory.</span></span>  

<span data-ttu-id="3167a-130">Siguiente ejecución Hola comandos de ejemplo de Hola repositorio y vaya toohello de tooclone *initialapp 0,1* de la versión.</span><span class="sxs-lookup"><span data-stu-id="3167a-130">Run hello following commands tooclone hello sample repository and go toohello *0.1-initialapp* release.</span></span>

```bash
git clone https://github.com/Azure-Samples/docker-flask-postgres.git
cd docker-flask-postgres
git checkout tags/0.1-initialapp
```

<span data-ttu-id="3167a-131">Este repositorio de ejemplo contiene una aplicación [Flask](http://flask.pocoo.org/).</span><span class="sxs-lookup"><span data-stu-id="3167a-131">This sample repository contains a [Flask](http://flask.pocoo.org/) application.</span></span> 

### <a name="run-hello-application"></a><span data-ttu-id="3167a-132">Ejecutar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="3167a-132">Run hello application</span></span>

> [!NOTE] 
> <span data-ttu-id="3167a-133">En un paso posterior simplifican este proceso mediante la creación de un toouse de contenedor de Docker con la base de datos de producción de hello.</span><span class="sxs-lookup"><span data-stu-id="3167a-133">In a later step you simplify this process by building a Docker container toouse with hello production database.</span></span>

<span data-ttu-id="3167a-134">Instalar paquetes de saludo necesario e inicie la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="3167a-134">Install hello required packages and start hello application.</span></span>

```bash
pip install virtualenv
virtualenv venv
source venv/bin/activate
pip install -r requirements.txt
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="3167a-135">Cuando se ha cargado completamente la aplicación hello, verá algo similar toohello siguiente mensaje:</span><span class="sxs-lookup"><span data-stu-id="3167a-135">When hello app is fully loaded, you see something similar toohello following message:</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C tooquit)
```

<span data-ttu-id="3167a-136">Navegue toohttp://127.0.0.1:5000 en un explorador.</span><span class="sxs-lookup"><span data-stu-id="3167a-136">Navigate toohttp://127.0.0.1:5000 in a browser.</span></span> <span data-ttu-id="3167a-137">Haga clic en **Register!** (Registrarse)</span><span class="sxs-lookup"><span data-stu-id="3167a-137">Click **Register!**</span></span> <span data-ttu-id="3167a-138">y cree un usuario de prueba.</span><span class="sxs-lookup"><span data-stu-id="3167a-138">and create a test user.</span></span>

![Aplicación Python Flask que se ejecuta de forma local](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

<span data-ttu-id="3167a-140">aplicación de ejemplo matraz Hola almacena datos de usuario de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="3167a-140">hello Flask sample application stores user data in hello database.</span></span> <span data-ttu-id="3167a-141">Si es correcta en el registro de un usuario, la aplicación está escribiendo la base de datos de PostgreSQL local de datos toohello.</span><span class="sxs-lookup"><span data-stu-id="3167a-141">If you are successful at registering a user, your app is writing data toohello local PostgreSQL database.</span></span>

<span data-ttu-id="3167a-142">tipo de servidor de toostop Hola matraz en cualquier momento, que Ctrl + C en hello terminal.</span><span class="sxs-lookup"><span data-stu-id="3167a-142">toostop hello Flask server at anytime, type Ctrl+C in hello terminal.</span></span> 

## <a name="create-a-production-postgresql-database"></a><span data-ttu-id="3167a-143">Creación de una base de datos PostgreSQL de producción</span><span class="sxs-lookup"><span data-stu-id="3167a-143">Create a production PostgreSQL database</span></span>

<span data-ttu-id="3167a-144">En este paso, creará una base de datos PostgreSQL en Azure.</span><span class="sxs-lookup"><span data-stu-id="3167a-144">In this step, you create a PostgreSQL database in Azure.</span></span> <span data-ttu-id="3167a-145">Cuando la aplicación esté implementada tooAzure, usará esta base de datos en la nube.</span><span class="sxs-lookup"><span data-stu-id="3167a-145">When your app is deployed tooAzure, it will use this cloud database.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="3167a-146">Inicie sesión en tooAzure</span><span class="sxs-lookup"><span data-stu-id="3167a-146">Log in tooAzure</span></span>

<span data-ttu-id="3167a-147">Son ahora necesitan de curso toouse hello Azure CLI 2.0 toocreate Hola recursos toohost la aplicación de Python en el servicio de aplicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="3167a-147">You are now going toouse hello Azure CLI 2.0 toocreate hello resources needed toohost your Python application in Azure App Service.</span></span>  <span data-ttu-id="3167a-148">Inicie sesión en la suscripción de Azure con hello tooyour [inicio de sesión de az](/cli/azure/#login) comando y siga hello en pantalla instrucciones.</span><span class="sxs-lookup"><span data-stu-id="3167a-148">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> 

```azurecli
az login 
``` 
   
### <a name="create-a-resource-group"></a><span data-ttu-id="3167a-149">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="3167a-149">Create a resource group</span></span>

<span data-ttu-id="3167a-150">Crear un [grupo de recursos](../azure-resource-manager/resource-group-overview.md) con hello [crear grupo az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="3167a-150">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with hello [az group create](/cli/azure/group#create).</span></span> 

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

<span data-ttu-id="3167a-151">Hello en el ejemplo siguiente se crea un grupo de recursos en la región del oeste de Estados Unidos de hello:</span><span class="sxs-lookup"><span data-stu-id="3167a-151">hello following example creates a resource group in hello West US region:</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West US"
```

<span data-ttu-id="3167a-152">Hola de uso [az de servicio de aplicaciones enumerar ubicaciones](/cli/azure/appservice#list-locations) ubicaciones disponibles toolist de comandos de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="3167a-152">Use hello [az appservice list-locations](/cli/azure/appservice#list-locations) Azure CLI command toolist available locations.</span></span>

### <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="3167a-153">Creación de un servidor de Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="3167a-153">Create an Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="3167a-154">Crear un servidor de PostgreSQL con hello [az postgres servidor crear](/cli/azure/documentdb#create) comando.</span><span class="sxs-lookup"><span data-stu-id="3167a-154">Create a PostgreSQL server with hello [az postgres server create](/cli/azure/documentdb#create) command.</span></span>

<span data-ttu-id="3167a-155">En hello siguiente comando, sustitúyalo por un nombre de servidor único para hello  *\<postgresql_name >* marcador de posición y un nombre de usuario para hello  *\<admin_username >* marcador de posición .</span><span class="sxs-lookup"><span data-stu-id="3167a-155">In hello following command, substitute a unique server name for hello *\<postgresql_name>* placeholder and a user name for hello *\<admin_username>* placeholder.</span></span> <span data-ttu-id="3167a-156">nombre del servidor Hola se usa como parte de su punto de conexión de PostgreSQL (`https://<postgresql_name>.postgres.database.azure.com`), por lo que el nombre de hello necesita toobe único en todos los servidores en Azure.</span><span class="sxs-lookup"><span data-stu-id="3167a-156">hello server name is used as part of your PostgreSQL endpoint (`https://<postgresql_name>.postgres.database.azure.com`), so hello name needs toobe unique across all servers in Azure.</span></span> <span data-ttu-id="3167a-157">nombre de usuario de Hello es para la cuenta de usuario de administrador de base de datos inicial de Hola.</span><span class="sxs-lookup"><span data-stu-id="3167a-157">hello user name is for hello initial database admin user account.</span></span> <span data-ttu-id="3167a-158">Son solicitada toopick una contraseña para este usuario.</span><span class="sxs-lookup"><span data-stu-id="3167a-158">You are prompted toopick a password for this user.</span></span>

```azurecli-interactive
az postgres server create --resource-group myResourceGroup --name <postgresql_name> --admin-user <admin_username>
```

<span data-ttu-id="3167a-159">Cuando se crea Hola base de datos de Azure para servidor PostgreSQL, Hola CLI de Azure muestra información toohello similar siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3167a-159">When hello Azure Database for PostgreSQL server is created, hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "administratorLogin": "<my_admin_username>",
  "fullyQualifiedDomainName": "<postgresql_name>.postgres.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforPostgreSQL/servers/<postgresql_name>",
  "location": "westus",
  "name": "<postgresql_name>",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capacity": 100,
    "family": null,
    "name": "PGSQLS3M100",
    "size": null,
    "tier": "Basic"
  },
  "sslEnforcement": null,
  "storageMb": 2048,
  "tags": null,
  "type": "Microsoft.DBforPostgreSQL/servers",
  "userVisibleState": "Ready",
  "version": null
}
```

### <a name="create-a-firewall-rule-for-hello-azure-database-for-postgresql-server"></a><span data-ttu-id="3167a-160">Crear una regla de firewall para hello base de datos de Azure para servidor de PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="3167a-160">Create a firewall rule for hello Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="3167a-161">Ejecute hello siguiendo la base de datos de Azure CLI comando tooallow access toohello de todas las direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="3167a-161">Run hello following Azure CLI command tooallow access toohello database from all IP addresses.</span></span>

```azurecli-interactive
az postgres server firewall-rule create --resource-group myResourceGroup --server-name <postgresql_name> --start-ip-address=0.0.0.0 --end-ip-address=255.255.255.255 --name AllowAllIPs
```

<span data-ttu-id="3167a-162">Hola CLI de Azure confirma la creación de reglas de firewall de hello con salida toohello similar siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3167a-162">hello Azure CLI confirms hello firewall rule creation with output similar toohello following example:</span></span>

```json
{
  "endIpAddress": "255.255.255.255",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforPostgreSQL/servers/<postgresql_name>/firewallRules/AllowAllIPs",
  "name": "AllowAllIPs",
  "resourceGroup": "myResourceGroup",
  "startIpAddress": "0.0.0.0",
  "type": "Microsoft.DBforPostgreSQL/servers/firewallRules"
}
```

## <a name="connect-your-python-flask-application-toohello-database"></a><span data-ttu-id="3167a-163">Conectarse a la base de datos de Python matraz aplicación toohello</span><span class="sxs-lookup"><span data-stu-id="3167a-163">Connect your Python Flask application toohello database</span></span>

<span data-ttu-id="3167a-164">En este paso, se conectará su toohello de aplicación de ejemplo base de datos de Azure matraz de Python para servidor PostgreSQL que ha creado.</span><span class="sxs-lookup"><span data-stu-id="3167a-164">In this step, you connect your Python Flask sample application toohello Azure Database for PostgreSQL server you created.</span></span>

### <a name="create-an-empty-database-and-set-up-a-new-database-application-user"></a><span data-ttu-id="3167a-165">Creación de una base de datos vacía y configuración de un nuevo usuario de la aplicación de base de datos</span><span class="sxs-lookup"><span data-stu-id="3167a-165">Create an empty database and set up a new database application user</span></span>

<span data-ttu-id="3167a-166">Cree un usuario de base de datos con acceso tooa único solo base de datos.</span><span class="sxs-lookup"><span data-stu-id="3167a-166">Create a database user with access tooa single database only.</span></span> <span data-ttu-id="3167a-167">Usará estos tooavoid credenciales entregar Hola aplicación acceso completo toohello servidor.</span><span class="sxs-lookup"><span data-stu-id="3167a-167">You'll use these credentials tooavoid giving hello application full access toohello server.</span></span>

<span data-ttu-id="3167a-168">Conectar la base de datos de toohello (se le pide la contraseña de administrador).</span><span class="sxs-lookup"><span data-stu-id="3167a-168">Connect toohello database (you're prompted for your admin password).</span></span>

```bash
psql -h <postgresql_name>.postgres.database.azure.com -U <my_admin_username>@<postgresql_name> postgres
```

<span data-ttu-id="3167a-169">Crear base de datos de Hola y de usuario de hello PostgreSQL CLI.</span><span class="sxs-lookup"><span data-stu-id="3167a-169">Create hello database and user from hello PostgreSQL CLI.</span></span>

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration toomanager;
```

<span data-ttu-id="3167a-170">Tipo de *\q* cliente de tooexit Hola PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="3167a-170">Type *\q* tooexit hello PostgreSQL client.</span></span>

### <a name="test-hello-application-locally-against-hello-azure-postgresql-database"></a><span data-ttu-id="3167a-171">Probar la aplicación hello localmente en la base de datos de Azure PostgreSQL de Hola</span><span class="sxs-lookup"><span data-stu-id="3167a-171">Test hello application locally against hello Azure PostgreSQL database</span></span> 

<span data-ttu-id="3167a-172">Si vuelve ahora toohello *aplicación* carpeta de hello clona el repositorio de Github, puede ejecutar aplicación de Python matraz hello mediante la actualización de las variables de entorno de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="3167a-172">Going back now toohello *app* folder of hello cloned Github repository, you can run hello Python Flask application by updating hello database environment variables.</span></span>

```bash
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="3167a-173">Cuando se ha cargado completamente la aplicación hello, verá algo similar toohello siguiente mensaje:</span><span class="sxs-lookup"><span data-stu-id="3167a-173">When hello app is fully loaded, you see something similar toohello following message:</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C tooquit)
```

<span data-ttu-id="3167a-174">Navegue toohttp://127.0.0.1:5000 en un explorador.</span><span class="sxs-lookup"><span data-stu-id="3167a-174">Navigate toohttp://127.0.0.1:5000 in a browser.</span></span> <span data-ttu-id="3167a-175">Haga clic en **Register!** (Registrarse)</span><span class="sxs-lookup"><span data-stu-id="3167a-175">Click **Register!**</span></span> <span data-ttu-id="3167a-176">y cree un registro de prueba.</span><span class="sxs-lookup"><span data-stu-id="3167a-176">and create a test registration.</span></span> <span data-ttu-id="3167a-177">Ahora se escribe toohello de datos en Azure.</span><span class="sxs-lookup"><span data-stu-id="3167a-177">You are now writing data toohello database in Azure.</span></span>

![Aplicación Python Flask que se ejecuta de forma local](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

### <a name="running-hello-application-from-a-docker-container"></a><span data-ttu-id="3167a-179">Ejecutar la aplicación hello desde un contenedor de Docker</span><span class="sxs-lookup"><span data-stu-id="3167a-179">Running hello application from a Docker Container</span></span>

<span data-ttu-id="3167a-180">Crear imagen de contenedor de Docker Hola.</span><span class="sxs-lookup"><span data-stu-id="3167a-180">Build hello Docker container image.</span></span>

```bash
cd ..
docker build -t flask-postgresql-sample .
```

<span data-ttu-id="3167a-181">Docker muestra una confirmación de que el contenedor de hello, se creó correctamente.</span><span class="sxs-lookup"><span data-stu-id="3167a-181">Docker displays a confirmation that it successfully created hello container.</span></span>

```bash
Successfully built 7548f983a36b
```

<span data-ttu-id="3167a-182">Agregar el archivo de la variable de entorno entorno variables tooan de base de datos *db.env*.</span><span class="sxs-lookup"><span data-stu-id="3167a-182">Add database environment variables tooan environment variable file *db.env*.</span></span> <span data-ttu-id="3167a-183">aplicación Hello conectará toohello base de datos de producción de PostgreSQL en Azure.</span><span class="sxs-lookup"><span data-stu-id="3167a-183">hello app will connect toohello PostgreSQL production database in Azure.</span></span>

```text
DBHOST="<postgresql_name>.postgres.database.azure.com"
DBUSER="manager@<postgresql_name>"
DBNAME="eventregistration"
DBPASS="supersecretpass"
```

<span data-ttu-id="3167a-184">Ejecute la aplicación hello desde dentro del contenedor de Docker de Hola.</span><span class="sxs-lookup"><span data-stu-id="3167a-184">Run hello app from within hello Docker container.</span></span> <span data-ttu-id="3167a-185">Hola siguiente comando Especifica el archivo de variables de entorno de Hola y asigna Hola predeterminado matraz puerto 5000 toolocal puerto 5000.</span><span class="sxs-lookup"><span data-stu-id="3167a-185">hello following command specifies hello environment variable file and maps hello default Flask port 5000 toolocal port 5000.</span></span>

```bash
docker run -it --env-file db.env -p 5000:5000 flask-postgresql-sample
```

<span data-ttu-id="3167a-186">salida de Hello es toowhat similar que vio anteriormente.</span><span class="sxs-lookup"><span data-stu-id="3167a-186">hello output is similar toowhat you saw earlier.</span></span> <span data-ttu-id="3167a-187">Sin embargo, migración de base de datos inicial de hello ya no necesita toobe realiza y, por tanto, se omite.</span><span class="sxs-lookup"><span data-stu-id="3167a-187">However, hello initial database migration no longer needs toobe performed and therefore is skipped.</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
 * Serving Flask app "app"
 * Running on http://0.0.0.0:5000/ (Press CTRL+C tooquit)
```

<span data-ttu-id="3167a-188">base de datos de Hello ya contiene el registro de hello que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="3167a-188">hello database already contains hello registration you created previously.</span></span>

![Aplicación Python Flask basada en contenedor Docker que se ejecuta de forma local](./media/app-service-web-tutorial-docker-python-postgresql-app/local-docker.png)

## <a name="upload-hello-docker-container-tooa-container-registry"></a><span data-ttu-id="3167a-190">Cargar registro de contenedor de hello Docker contenedor tooa</span><span class="sxs-lookup"><span data-stu-id="3167a-190">Upload hello Docker container tooa container registry</span></span>

<span data-ttu-id="3167a-191">En este paso, se carga del registro de contenedor de hello Docker contenedor tooa.</span><span class="sxs-lookup"><span data-stu-id="3167a-191">In this step, you upload hello Docker container tooa container registry.</span></span> <span data-ttu-id="3167a-192">Se usará Azure Container Registry, pero también se pueden usar otros registros conocidos, como Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="3167a-192">You'll use Azure Container Registry, but you could also use other popular ones such as Docker Hub.</span></span>

### <a name="create-an-azure-container-registry"></a><span data-ttu-id="3167a-193">Creación de una instancia de Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="3167a-193">Create an Azure Container Registry</span></span>

<span data-ttu-id="3167a-194">Hola después de un registro de contenedor del comando toocreate reemplazar  *\<registry_name >* con un nombre de contenedor de Azure único del registro de su elección.</span><span class="sxs-lookup"><span data-stu-id="3167a-194">In hello following command toocreate a container registry replace *\<registry_name>* with a unique Azure container registry name of your choice.</span></span>

```azurecli-interactive
az acr create --name <registry_name> --resource-group myResourceGroup --location "West US" --sku Basic
```

<span data-ttu-id="3167a-195">Salida</span><span class="sxs-lookup"><span data-stu-id="3167a-195">Output</span></span>
```json
{
  "adminUserEnabled": false,
  "creationDate": "2017-05-04T08:50:55.635688+00:00",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/<registry_name>",
  "location": "westus",
  "loginServer": "<registry_name>.azurecr.io",
  "name": "<registry_name>",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "<registry_name>01234"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

### <a name="retrieve-hello-registry-credentials-for-pushing-and-pulling-docker-images"></a><span data-ttu-id="3167a-196">Recuperar las credenciales del registro de hello para insertar y extraer imágenes de Docker</span><span class="sxs-lookup"><span data-stu-id="3167a-196">Retrieve hello registry credentials for pushing and pulling Docker images</span></span>

<span data-ttu-id="3167a-197">las credenciales del registro de tooshow, habilite el modo de administrador en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="3167a-197">tooshow registry credentials, enable admin mode first.</span></span>

```azurecli-interactive
az acr update --name <registry_name> --admin-enabled true
az acr credential show -n <registry_name>
```

<span data-ttu-id="3167a-198">Verá dos contraseñas.</span><span class="sxs-lookup"><span data-stu-id="3167a-198">You see two passwords.</span></span> <span data-ttu-id="3167a-199">Tome nota del nombre de usuario de Hola y la contraseña primera Hola.</span><span class="sxs-lookup"><span data-stu-id="3167a-199">Make note of hello user name and hello first password.</span></span>

```json
{
  "passwords": [
    {
      "name": "password",
      "value": "<registry_password>"
    },
    {
      "name": "password2",
      "value": "<registry_password2>"
    }
  ],
  "username": "<registry_name>"
}
```

### <a name="upload-your-docker-container-tooazure-container-registry"></a><span data-ttu-id="3167a-200">Cargar su tooAzure de contenedor del registro de contenedor de Docker</span><span class="sxs-lookup"><span data-stu-id="3167a-200">Upload your Docker container tooAzure Container Registry</span></span>

```bash
docker login <registry_name>.azurecr.io -u <registry_name> -p "<registry_password>"
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
```

## <a name="deploy-hello-docker-python-flask-application-tooazure"></a><span data-ttu-id="3167a-201">Implementar hello Docker Python matraz aplicación tooAzure</span><span class="sxs-lookup"><span data-stu-id="3167a-201">Deploy hello Docker Python Flask application tooAzure</span></span>

<span data-ttu-id="3167a-202">En este paso, implementará la tooAzure de aplicación en la matraz de Python en el basado en el contenedor de Docker servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="3167a-202">In this step, you deploy your Docker container-based Python Flask application tooAzure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="3167a-203">Creación de un plan de App Service</span><span class="sxs-lookup"><span data-stu-id="3167a-203">Create an App Service plan</span></span>

<span data-ttu-id="3167a-204">Crear un plan de servicio de aplicaciones con hello [Crear plan de servicio de aplicaciones az](/cli/azure/appservice/plan#create) comando.</span><span class="sxs-lookup"><span data-stu-id="3167a-204">Create an App Service plan with hello [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="3167a-205">Hello en el ejemplo siguiente se crea un plan de servicio de aplicaciones basadas en Linux denominado *myAppServicePlan* con hello S1 tarifa:</span><span class="sxs-lookup"><span data-stu-id="3167a-205">hello following example creates a Linux-based App Service plan named *myAppServicePlan* using hello S1 pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku S1 --is-linux
```

<span data-ttu-id="3167a-206">Cuando se crea el plan de servicio de aplicación Hola, Hola CLI de Azure muestra información toohello similar siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3167a-206">When hello App Service plan is created, hello Azure CLI shows information similar toohello following example:</span></span>

```json 
{
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "West US",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
  "kind": "linux",
  "location": "West US",
  "maximumNumberOfWorkers": 10,
  "name": "myAppServicePlan",
  "numberOfSites": 0,
  "perSiteScaling": false,
  "provisioningState": "Succeeded",
  "reserved": true,
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capabilities": null,
    "capacity": 1,
    "family": "S",
    "locations": null,
    "name": "S1",
    "size": "S1",
    "skuCapacity": null,
    "tier": "Standard"
  },
  "status": "Ready",
  "subscription": "00000000-0000-0000-0000-000000000000",
  "tags": null,
  "targetWorkerCount": 0,
  "targetWorkerSizeId": 0,
  "type": "Microsoft.Web/serverfarms",
  "workerTierName": null
}
``` 

### <a name="create-a-web-app"></a><span data-ttu-id="3167a-207">Creación de una aplicación web</span><span class="sxs-lookup"><span data-stu-id="3167a-207">Create a web app</span></span>

<span data-ttu-id="3167a-208">Crear una aplicación web en hello *myAppServicePlan* plan de servicio de aplicaciones con hello [crear webapp az](/cli/azure/webapp#create) comando.</span><span class="sxs-lookup"><span data-stu-id="3167a-208">Create a web app in hello *myAppServicePlan* App Service plan with hello [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="3167a-209">Hola web aplicación le ofrece un hospedaje espacio toodeploy el código y proporciona una dirección URL de hello tooview implementado la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3167a-209">hello web app gives you a hosting space toodeploy your code and provides a URL for you tooview hello deployed application.</span></span> <span data-ttu-id="3167a-210">Aplicación web de uso toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="3167a-210">Use  toocreate hello web app.</span></span> 

<span data-ttu-id="3167a-211">Hola el siguiente comando, reemplace hello  *\<app_name >* marcador de posición con un nombre de aplicación único.</span><span class="sxs-lookup"><span data-stu-id="3167a-211">In hello following command, replace hello *\<app_name>* placeholder with a unique app name.</span></span> <span data-ttu-id="3167a-212">Este nombre forma parte de la dirección URL predeterminada de hello para la aplicación web de hello, por lo que el nombre de hello necesita toobe único en todas las aplicaciones de servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="3167a-212">This name is part of hello default URL for hello web app, so hello name needs toobe unique across all apps in Azure App Service.</span></span> 

```azurecli
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="3167a-213">Cuando se ha creado la aplicación web de hello, Hola CLI de Azure muestra información toohello similar siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3167a-213">When hello web app has been created, hello Azure CLI shows information similar toohello following example:</span></span> 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
  ...
  < Output has been truncated for readability >
}
```

### <a name="configure-hello-database-environment-variables"></a><span data-ttu-id="3167a-214">Configurar las variables de entorno de base de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="3167a-214">Configure hello database environment variables</span></span>

<span data-ttu-id="3167a-215">Anteriormente en el tutorial de hello, ha definido la base de datos PostgreSQL tooyour de tooconnect de variables de entorno.</span><span class="sxs-lookup"><span data-stu-id="3167a-215">Earlier in hello tutorial, you defined environment variables tooconnect tooyour PostgreSQL database.</span></span>

<span data-ttu-id="3167a-216">En el servicio de aplicación, establecer variables de entorno como _configuración de la aplicación_ mediante el uso de hello [az webapp configuración appsettings conjunto](/cli/azure/webapp/config#set) comando.</span><span class="sxs-lookup"><span data-stu-id="3167a-216">In App Service, you set environment variables as _app settings_ by using hello [az webapp config appsettings set](/cli/azure/webapp/config#set) command.</span></span> 

<span data-ttu-id="3167a-217">Hello en el ejemplo siguiente se especifica detalles de conexión de base de datos de hello como configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3167a-217">hello following example specifies hello database connection details as app settings.</span></span> <span data-ttu-id="3167a-218">También usa hello *puerto* variable toomap puerto 5000 desde el tráfico de contenedor Docker tooreceive HTTP en el puerto 80.</span><span class="sxs-lookup"><span data-stu-id="3167a-218">It also uses hello *PORT* variable toomap PORT 5000 from your Docker Container tooreceive HTTP traffic on PORT 80.</span></span>

```azurecli-interactive
az webapp config appsettings set --name <app_name> --resource-group myResourceGroup --settings DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBPASS="supersecretpass" DBNAME="eventregistration" PORT=5000
```

### <a name="configure-docker-container-deployment"></a><span data-ttu-id="3167a-219">Configuración de la implementación del contenedor de Docker</span><span class="sxs-lookup"><span data-stu-id="3167a-219">Configure Docker container deployment</span></span> 

<span data-ttu-id="3167a-220">App Service puede descargar automáticamente un contenedor de Docker y ejecutarlo.</span><span class="sxs-lookup"><span data-stu-id="3167a-220">AppService can automatically download and run a Docker container.</span></span>

```azurecli
az webapp config container set --resource-group myResourceGroup --name <app_name> --docker-registry-server-user "<registry_name>" --docker-registry-server-password "<registry_password>" --docker-custom-image-name "<registry_name>.azurecr.io/flask-postgresql-sample" --docker-registry-server-url "https://<registry_name>.azurecr.io"
```

<span data-ttu-id="3167a-221">Siempre que actualiza el contenedor de Docker de Hola o cambia la configuración de hello, reinicie la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="3167a-221">Whenever you update hello Docker container or change hello settings, restart hello app.</span></span> <span data-ttu-id="3167a-222">Reiniciar, se garantiza que todas las configuraciones se aplican y contenedor más reciente de Hola se extrae del registro de hello.</span><span class="sxs-lookup"><span data-stu-id="3167a-222">Restarting ensures that all settings are applied and hello latest container is pulled from hello registry.</span></span>

```azurecli-interactive
az webapp restart --resource-group myResourceGroup --name <app_name>
```

### <a name="browse-toohello-azure-web-app"></a><span data-ttu-id="3167a-223">Examinar la aplicación web de Azure de toohello</span><span class="sxs-lookup"><span data-stu-id="3167a-223">Browse toohello Azure web app</span></span> 

<span data-ttu-id="3167a-224">Examinar toohello implementa la aplicación web mediante el explorador web.</span><span class="sxs-lookup"><span data-stu-id="3167a-224">Browse toohello deployed web app using your web browser.</span></span> 

```bash 
http://<app_name>.azurewebsites.net 
```
> [!NOTE]
> <span data-ttu-id="3167a-225">aplicación web de Hello tiene más tooload como contenedor de hello tiene toobe descargará y se iniciará después de cambia la configuración del contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="3167a-225">hello web app takes longer tooload because hello container has toobe downloaded and started after hello container configuration is changed.</span></span>

<span data-ttu-id="3167a-226">Vea a invitados previamente registrados que se guardaron toohello base de datos de producción de Azure en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="3167a-226">You see previously registered guests that were saved toohello Azure production database in hello previous step.</span></span>

![Aplicación Python Flask basada en contenedor Docker que se ejecuta de forma local](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-app-deployed.png)

<span data-ttu-id="3167a-228">**¡Enhorabuena!**</span><span class="sxs-lookup"><span data-stu-id="3167a-228">**Congratulations!**</span></span> <span data-ttu-id="3167a-229">Ya está ejecutando una aplicación Python Flask basada en contenedor en Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="3167a-229">You're running a Docker container-based Python Flask app in Azure App Service.</span></span>

## <a name="update-data-model-and-redeploy"></a><span data-ttu-id="3167a-230">Actualización del modelo de datos y nueva implementación</span><span class="sxs-lookup"><span data-stu-id="3167a-230">Update data model and redeploy</span></span>

<span data-ttu-id="3167a-231">En este paso es agregar el número de hello asistentes tooeach del registro de eventos mediante la actualización de modelo de invitado de Hola.</span><span class="sxs-lookup"><span data-stu-id="3167a-231">In this step, you add hello number of attendees tooeach event registration by updating hello Guest model.</span></span>

<span data-ttu-id="3167a-232">Extraer del repositorio hello *0,2 migración* versión con el siguiente comando de git de hello:</span><span class="sxs-lookup"><span data-stu-id="3167a-232">Check out hello *0.2-migration* release with hello following git command:</span></span>

```bash
git checkout tags/0.2-migration
```

<span data-ttu-id="3167a-233">Esta versión ya realizada Hola modelo, los controladores y tooviews cambios necesarios.</span><span class="sxs-lookup"><span data-stu-id="3167a-233">This release already made hello necessary changes tooviews, controllers, and model.</span></span> <span data-ttu-id="3167a-234">También incluye una migración de base de datos generada mediante *alembic* (`flask db migrate`).</span><span class="sxs-lookup"><span data-stu-id="3167a-234">It also includes a database migration generated via *alembic* (`flask db migrate`).</span></span> <span data-ttu-id="3167a-235">Puede ver todos los cambios realizados a través del siguiente comando de git de hello:</span><span class="sxs-lookup"><span data-stu-id="3167a-235">You can see all changes made via hello following git command:</span></span>

```bash
git diff 0.1-initialapp 0.2-migration
```

### <a name="test-your-changes-locally"></a><span data-ttu-id="3167a-236">Prueba de los cambios localmente</span><span class="sxs-lookup"><span data-stu-id="3167a-236">Test your changes locally</span></span>

<span data-ttu-id="3167a-237">Ejecute hello después comandos tootest los cambios localmente por servidor en ejecución Hola matraz.</span><span class="sxs-lookup"><span data-stu-id="3167a-237">Run hello following commands tootest your changes locally by running hello flask server.</span></span>

<span data-ttu-id="3167a-238">Mac o Linux:</span><span class="sxs-lookup"><span data-stu-id="3167a-238">Mac / Linux:</span></span>
```bash
source venv/bin/activate
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="3167a-239">Navegue toohttp://127.0.0.1:5000 los cambios de hello tooview de explorador.</span><span class="sxs-lookup"><span data-stu-id="3167a-239">Navigate toohttp://127.0.0.1:5000 in your browser tooview hello changes.</span></span> <span data-ttu-id="3167a-240">Cree un registro de prueba.</span><span class="sxs-lookup"><span data-stu-id="3167a-240">Create a test registration.</span></span>

![Aplicación Python Flask basada en contenedor Docker que se ejecuta de forma local](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app-v2.png)

### <a name="publish-changes-tooazure"></a><span data-ttu-id="3167a-242">Publicar cambios tooAzure</span><span class="sxs-lookup"><span data-stu-id="3167a-242">Publish changes tooAzure</span></span>

<span data-ttu-id="3167a-243">Crear nueva imagen de docker Hola, Insertar registro de contenedor de toohello y reiniciar la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="3167a-243">Build hello new docker image, push it toohello container registry, and restart hello app.</span></span>

```bash
docker build -t flask-postgresql-sample .
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
az appservice web restart --resource-group myResourceGroup --name <app_name>
```

<span data-ttu-id="3167a-244">Navegar por la aplicación web de Azure de tooyour e inténtelo de nuevo funcionalidad nueva de Hola.</span><span class="sxs-lookup"><span data-stu-id="3167a-244">Navigate tooyour Azure web app and try out hello new functionality again.</span></span> <span data-ttu-id="3167a-245">Cree otro registro de eventos.</span><span class="sxs-lookup"><span data-stu-id="3167a-245">Create another event registration.</span></span>

```bash 
http://<app_name>.azurewebsites.net 
```

![Aplicación Docker Python Flask en Azure App Service](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="3167a-247">Administración de la aplicación web de Azure</span><span class="sxs-lookup"><span data-stu-id="3167a-247">Manage your Azure web app</span></span>

<span data-ttu-id="3167a-248">Vaya toohello [portal de Azure](https://portal.azure.com) toosee hello web aplicación que creó.</span><span class="sxs-lookup"><span data-stu-id="3167a-248">Go toohello [Azure portal](https://portal.azure.com) toosee hello web app you created.</span></span>

<span data-ttu-id="3167a-249">Hola menú izquierdo, haga clic en **servicios de aplicaciones**, a continuación, haga clic en nombre de saludo de la aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="3167a-249">From hello left menu, click **App Services**, then click hello name of your Azure web app.</span></span>

![Aplicación de navegación del portal tooAzure web](./media/app-service-web-tutorial-docker-python-postgresql-app/app-resource.png)

<span data-ttu-id="3167a-251">De forma predeterminada, el portal de hello muestra la aplicación web **Introducción** página.</span><span class="sxs-lookup"><span data-stu-id="3167a-251">By default, hello portal shows your web app's **Overview** page.</span></span> <span data-ttu-id="3167a-252">Esta página proporciona una visión del funcionamiento de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3167a-252">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="3167a-253">En este caso, también puede realizar tareas de administración básicas como examinar, detener, iniciar, reiniciar y eliminar.</span><span class="sxs-lookup"><span data-stu-id="3167a-253">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="3167a-254">pestañas: Hola a la izquierda Hola de página Hola páginas de configuración diferente de hello que puede abrir.</span><span class="sxs-lookup"><span data-stu-id="3167a-254">hello tabs on hello left side of hello page show hello different configuration pages you can open.</span></span>

![Página de App Service en Azure Portal](./media/app-service-web-tutorial-docker-python-postgresql-app/app-mgmt.png)

## <a name="next-steps"></a><span data-ttu-id="3167a-256">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3167a-256">Next steps</span></span>

<span data-ttu-id="3167a-257">Avanzar toohello siguiente tutorial toolearn cómo toomap un DNS personalizado nombre tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="3167a-257">Advance toohello next tutorial toolearn how toomap a custom DNS name tooyour web app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="3167a-258">Asignar un tooAzure de nombre DNS personalizado existente aplicaciones Web</span><span class="sxs-lookup"><span data-stu-id="3167a-258">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
