---
title: "Compilación de una aplicación web Java y MySQL en Azure"
description: "Aprenda a conseguir que una aplicación Java se conecte al servicio de la base de datos MySQL de Azure y que funcione en un servicio de aplicaciones de Azure."
services: app-service\web
documentationcenter: Java
author: bbenz
manager: jeffsand
editor: jasonwhowell
ms.assetid: 
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: tutorial
ms.date: 05/22/2017
ms.author: bbenz
ms.custom: mvc
ms.openlocfilehash: eb2d59939c4e4486bb14bb143a4a18f9bc1478e1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="build-a-java-and-mysql-web-app-in-azure"></a><span data-ttu-id="930dd-103">Compilación de una aplicación web Java y MySQL en Azure</span><span class="sxs-lookup"><span data-stu-id="930dd-103">Build a Java and MySQL web app in Azure</span></span>

<span data-ttu-id="930dd-104">En este tutorial se muestra cómo crear una aplicación web Java en Azure y conectarla a una base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="930dd-104">This tutorial shows you how to create a Java web app in Azure and connect it to a MySQL database.</span></span> <span data-ttu-id="930dd-105">Cuando haya terminado, tendrá una aplicación [Spring Boot](https://projects.spring.io/spring-boot/) que almacena datos en [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) y que se ejecuta en [Azure App Service Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).</span><span class="sxs-lookup"><span data-stu-id="930dd-105">When you are finished, you will have a [Spring Boot](https://projects.spring.io/spring-boot/) application storing data in [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) running on [Azure App Service Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).</span></span>

![Aplicación Java que se ejecuta en Azure App Service](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

<span data-ttu-id="930dd-107">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="930dd-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="930dd-108">Crear una base de datos MySQL en Azure</span><span class="sxs-lookup"><span data-stu-id="930dd-108">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="930dd-109">Conectar una aplicación de ejemplo a la base de datos</span><span class="sxs-lookup"><span data-stu-id="930dd-109">Connect a sample app to the database</span></span>
> * <span data-ttu-id="930dd-110">Implementación de la aplicación en Azure</span><span class="sxs-lookup"><span data-stu-id="930dd-110">Deploy the app to Azure</span></span>
> * <span data-ttu-id="930dd-111">Actualización de la aplicación y nueva implementación</span><span class="sxs-lookup"><span data-stu-id="930dd-111">Update and redeploy the app</span></span>
> * <span data-ttu-id="930dd-112">Transmitir registros de diagnóstico desde Azure</span><span class="sxs-lookup"><span data-stu-id="930dd-112">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="930dd-113">Supervisar la aplicación en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="930dd-113">Monitor the app in the Azure portal</span></span>


## <a name="prerequisites"></a><span data-ttu-id="930dd-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="930dd-114">Prerequisites</span></span>

1. [<span data-ttu-id="930dd-115">Descarga e instalación de Git</span><span class="sxs-lookup"><span data-stu-id="930dd-115">Download and install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="930dd-116">Descarga e instalación de Java 7 JDK o superior</span><span class="sxs-lookup"><span data-stu-id="930dd-116">Download and install the Java 7 JDK or above</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
1. [<span data-ttu-id="930dd-117">Descarga, instalación e inicio de MySQL</span><span class="sxs-lookup"><span data-stu-id="930dd-117">Download, install, and start MySQL</span></span>](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="930dd-118">Si decide instalar y usar la CLI localmente, para este tema es preciso que ejecute la CLI de Azure versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="930dd-118">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="930dd-119">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="930dd-119">Run `az --version` to find the version.</span></span> <span data-ttu-id="930dd-120">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="930dd-120">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-local-mysql"></a><span data-ttu-id="930dd-121">Preparación de MySQL local</span><span class="sxs-lookup"><span data-stu-id="930dd-121">Prepare local MySQL</span></span> 

<span data-ttu-id="930dd-122">En este paso, creará una base de datos en un servidor MySQL local para usarlo al probar la aplicación localmente en la máquina.</span><span class="sxs-lookup"><span data-stu-id="930dd-122">In this step, you create a database in a local MySQL server for use in testing the app locally on your machine.</span></span>

### <a name="connect-to-mysql-server"></a><span data-ttu-id="930dd-123">Conexión a un servidor MySQL</span><span class="sxs-lookup"><span data-stu-id="930dd-123">Connect to MySQL server</span></span>

<span data-ttu-id="930dd-124">En una ventana de terminal, conéctese al servidor MySQL local.</span><span class="sxs-lookup"><span data-stu-id="930dd-124">In a terminal window, connect to your local MySQL server.</span></span> <span data-ttu-id="930dd-125">Esta ventana de terminal se puede usar para ejecutar todos los comandos de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="930dd-125">You can use this terminal window to run all the commands in this tutorial.</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="930dd-126">Si se le pide una contraseña, escriba la de la cuenta `root`.</span><span class="sxs-lookup"><span data-stu-id="930dd-126">If you're prompted for a password, enter the password for the `root` account.</span></span> <span data-ttu-id="930dd-127">Si no recuerda la contraseña de la cuenta raíz, consulte [MySQL: How to Reset the Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html) (MySQL: Instrucciones de restablecimiento de la contraseña de la cuenta raíz).</span><span class="sxs-lookup"><span data-stu-id="930dd-127">If you don't remember your root account password, see [MySQL: How to Reset the Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span></span>

<span data-ttu-id="930dd-128">Si el comando se ejecuta correctamente, significa que el servidor MySQL ya se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="930dd-128">If your command runs successfully, then your MySQL server is already running.</span></span> <span data-ttu-id="930dd-129">De lo contrario, siga los [pasos posteriores a la instalación de MySQL](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html) para asegurarse de iniciar el servidor local de MySQL.</span><span class="sxs-lookup"><span data-stu-id="930dd-129">If not, make sure that your local MySQL server is started by following the [MySQL post-installation steps](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span></span>

### <a name="create-a-database"></a><span data-ttu-id="930dd-130">Creación de una base de datos</span><span class="sxs-lookup"><span data-stu-id="930dd-130">Create a database</span></span> 

<span data-ttu-id="930dd-131">En el símbolo del sistema `mysql`, cree una base de datos y una tabla para los elementos pendientes.</span><span class="sxs-lookup"><span data-stu-id="930dd-131">In the `mysql` prompt, create a database and a table for the to-do items.</span></span>

```sql
CREATE DATABASE tododb;
```

<span data-ttu-id="930dd-132">Escriba `quit` para salir de la conexión del servidor.</span><span class="sxs-lookup"><span data-stu-id="930dd-132">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="create-and-run-the-sample-app"></a><span data-ttu-id="930dd-133">Creación y ejecución de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="930dd-133">Create and run the sample app</span></span> 

<span data-ttu-id="930dd-134">En este paso, va a clonar una aplicación de Spring Boot de ejemplo, la va a configurar para utilizar la base de datos MySQL local y la ejecutará en el equipo.</span><span class="sxs-lookup"><span data-stu-id="930dd-134">In this step, you clone sample Spring boot app, configure it to use the local MySQL database, and run it on your computer.</span></span> 

### <a name="clone-the-sample"></a><span data-ttu-id="930dd-135">Clonación del ejemplo</span><span class="sxs-lookup"><span data-stu-id="930dd-135">Clone the sample</span></span>

<span data-ttu-id="930dd-136">En la ventana de terminal, vaya a un directorio de trabajo y clone el repositorio de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="930dd-136">In the terminal window, navigate to a working directory and clone the sample repository.</span></span> 

```bash
git clone https://github.com/azure-samples/mysql-spring-boot-todo
```

### <a name="configure-the-app-to-use-the-mysql-database"></a><span data-ttu-id="930dd-137">Configuración de la aplicación para que use la base de datos de MySQL</span><span class="sxs-lookup"><span data-stu-id="930dd-137">Configure the app to use the MySQL database</span></span>

<span data-ttu-id="930dd-138">Actualice el valor `spring.datasource.password` en *spring-boot-mysql-todo/src/main/resources/application.properties* con la misma contraseña raíz usada para abrir el símbolo del sistema de MySQL:</span><span class="sxs-lookup"><span data-stu-id="930dd-138">Update the `spring.datasource.password` and  value in *spring-boot-mysql-todo/src/main/resources/application.properties* with the same root password used to open the MySQL prompt:</span></span>

```
spring.datasource.password=mysqlpass
```

### <a name="build-and-run-the-sample"></a><span data-ttu-id="930dd-139">Compilación y ejecución del ejemplo</span><span class="sxs-lookup"><span data-stu-id="930dd-139">Build and run the sample</span></span>

<span data-ttu-id="930dd-140">Compile y ejecute el ejemplo mediante el contenedor de Maven incluido en el repositorio:</span><span class="sxs-lookup"><span data-stu-id="930dd-140">Build and run the sample using the Maven wrapper included in the repo:</span></span>

```bash
cd spring-boot-mysql-todo
mvnw package spring-boot:run
```

<span data-ttu-id="930dd-141">Abra el explorador en http://localhost:8080 para ver el ejemplo en acción.</span><span class="sxs-lookup"><span data-stu-id="930dd-141">Open your browser to http://localhost:8080 to see in the sample in action.</span></span> <span data-ttu-id="930dd-142">A medida que agrega tareas a la lista, utilice los siguientes comandos SQL de la línea de comandos de MySQL para ver los datos almacenados en MySQL.</span><span class="sxs-lookup"><span data-stu-id="930dd-142">As you add tasks to the list,  use the following SQL commands in the MySQL prompt to view the data stored in MySQL.</span></span>

```SQL
use testdb;
select * from todo_item;
```

<span data-ttu-id="930dd-143">Detenga la aplicación presionando `Ctrl`+`C` en el terminal.</span><span class="sxs-lookup"><span data-stu-id="930dd-143">Stop the application by hitting `Ctrl`+`C` in the terminal.</span></span> 

## <a name="create-an-azure-mysql-database"></a><span data-ttu-id="930dd-144">Creación de una base de datos MySQL de Azure</span><span class="sxs-lookup"><span data-stu-id="930dd-144">Create an Azure MySQL database</span></span>

<span data-ttu-id="930dd-145">En este paso, va a crear una instancia de [Azure Database for MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) mediante la [CLI de Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="930dd-145">In this step, you create an [Azure Database for MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) instance using the [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="930dd-146">Va a configurar la aplicación de ejemplo para usar esta base de datos más adelante en el tutorial.</span><span class="sxs-lookup"><span data-stu-id="930dd-146">You configure the sample application to use this database later on in the tutorial.</span></span>

<span data-ttu-id="930dd-147">Use la CLI de Azure 2.0 en una ventana de terminal para crear los recursos necesarios para hospedar la aplicación Java en Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="930dd-147">Use the Azure CLI 2.0 in a terminal window to create the resources needed to host your Java application in Azure appservice.</span></span> <span data-ttu-id="930dd-148">Inicie sesión en la suscripción de Azure con el comando [az login](/cli/azure/#login) y siga las instrucciones de la pantalla.</span><span class="sxs-lookup"><span data-stu-id="930dd-148">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span> 

```azurecli-interactive 
az login 
```   

### <a name="create-a-resource-group"></a><span data-ttu-id="930dd-149">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="930dd-149">Create a resource group</span></span>

<span data-ttu-id="930dd-150">Cree un [grupo de recursos](../azure-resource-manager/resource-group-overview.md) con el comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="930dd-150">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="930dd-151">Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y administran recursos relacionados como aplicaciones web, bases de datos y cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="930dd-151">An Azure resource group is a logical container where related resources like web apps, databases, and storage accounts are deployed and managed.</span></span> 

<span data-ttu-id="930dd-152">En el siguiente ejemplo, se crea un grupo de recursos en la región de Europa del Norte:</span><span class="sxs-lookup"><span data-stu-id="930dd-152">The following example creates a resource group in the North Europe region:</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "North Europe"
```    

<span data-ttu-id="930dd-153">Para ver los valores posibles que puede usar para `--location`, use el comando [az appservice list-locations](/cli/azure/appservice#list-locations).</span><span class="sxs-lookup"><span data-stu-id="930dd-153">To see the possible values you can use for `--location`, use the [az appservice list-locations](/cli/azure/appservice#list-locations) command.</span></span>

### <a name="create-a-mysql-server"></a><span data-ttu-id="930dd-154">Creación de un servidor MySQL</span><span class="sxs-lookup"><span data-stu-id="930dd-154">Create a MySQL server</span></span>

<span data-ttu-id="930dd-155">Cree un servidor en Azure Database for MySQL (versión preliminar) con el comando [az mysql server create](/cli/azure/mysql/server#create).</span><span class="sxs-lookup"><span data-stu-id="930dd-155">Create a server in Azure Database for MySQL (Preview) with the [az mysql server create](/cli/azure/mysql/server#create) command.</span></span>    
<span data-ttu-id="930dd-156">Reemplace su nombre de servidor MySQL único donde vea el marcador de posición `<mysql_server_name>`.</span><span class="sxs-lookup"><span data-stu-id="930dd-156">Substitute your own unique MySQL server name where you see the `<mysql_server_name>` placeholder.</span></span> <span data-ttu-id="930dd-157">Este nombre forma parte del nombre de host del servidor MySQL, `<mysql_server_name>.mysql.database.azure.com`, por lo que debe ser único.</span><span class="sxs-lookup"><span data-stu-id="930dd-157">This name is part of your MySQL server's hostname, `<mysql_server_name>.mysql.database.azure.com`, so it needs to be globally unique.</span></span> <span data-ttu-id="930dd-158">Reemplace también `<admin_user>` y `<admin_password>` por sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="930dd-158">Also substitute `<admin_user>` and `<admin_password>` with your own values.</span></span>

```azurecli-interactive
az mysql server create --name <mysql_server_name> \ 
    --resource-group myResourceGroup \ 
    --location "North Europe" \
    --admin-user <admin_user> \ 
    --admin-password <admin_password>
```

<span data-ttu-id="930dd-159">Cuando se crea el servidor MySQL, la CLI de Azure muestra información similar a la del siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="930dd-159">When the MySQL server is created, the Azure CLI shows information similar to the following example:</span></span>

```json
{
  "administratorLogin": "admin_user",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "mysql_server_name.mysql.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforMySQL/servers/mysql_server_name",
  "location": "northeurope",
  "name": "mysql_server_name",
  "resourceGroup": "mysqlJavaResourceGroup",
  ...
  < Output has been truncated for readability >
}
```

### <a name="configure-server-firewall"></a><span data-ttu-id="930dd-160">Configuración del firewall del servidor</span><span class="sxs-lookup"><span data-stu-id="930dd-160">Configure server firewall</span></span>

<span data-ttu-id="930dd-161">Cree una regla de firewall para que el servidor MySQL permita conexiones de clientes usando el comando [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create).</span><span class="sxs-lookup"><span data-stu-id="930dd-161">Create a firewall rule for your MySQL server to allow client connections by using the [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create) command.</span></span> 

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name>  \ 
    --resource-group myResourceGroup \ 
    --start-ip-address 0.0.0.0 \ 
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="930dd-162">Azure Database for MySQL (versión preliminar) no permite en este momento habilitar conexiones automáticamente desde servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="930dd-162">Azure Database for MySQL (Preview) does not currently automatically enable connections from Azure services.</span></span> <span data-ttu-id="930dd-163">Dado que las direcciones IP se asignan de forma dinámica en Azure, es mejor habilitarlas todas por el momento.</span><span class="sxs-lookup"><span data-stu-id="930dd-163">As IP addresses in Azure are dynamically assigned, it is better to enable all IP addresses for now.</span></span> <span data-ttu-id="930dd-164">Como el servicio continúa en versión preliminar, se habilitarán métodos mejores para proteger la base de datos.</span><span class="sxs-lookup"><span data-stu-id="930dd-164">As the service continues its preview, better methods for securing your database will be enabled.</span></span>

## <a name="configure-the-azure-mysql-database"></a><span data-ttu-id="930dd-165">Configuración de la base de datos MySQL de Azure</span><span class="sxs-lookup"><span data-stu-id="930dd-165">Configure the Azure MySQL database</span></span>

<span data-ttu-id="930dd-166">En la ventana de terminal, en el equipo, conéctese al servidor MySQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="930dd-166">In the terminal window on your computer, connect to the MySQL server in Azure.</span></span> <span data-ttu-id="930dd-167">Use el valor que especificó anteriormente para `<admin_user>` y `<mysql_server_name>`.</span><span class="sxs-lookup"><span data-stu-id="930dd-167">Use the value you specified previously for `<admin_user>` and `<mysql_server_name>`.</span></span>

```bash
mysql -u <admin_user>@<mysql_server_name> -h <mysql_server_name>.mysql.database.azure.com -P 3306 -p
```

### <a name="create-a-database"></a><span data-ttu-id="930dd-168">Creación de una base de datos</span><span class="sxs-lookup"><span data-stu-id="930dd-168">Create a database</span></span> 

<span data-ttu-id="930dd-169">En el símbolo del sistema `mysql`, cree una base de datos y una tabla para los elementos pendientes.</span><span class="sxs-lookup"><span data-stu-id="930dd-169">In the `mysql` prompt, create a database and a table for the to-do items.</span></span>

```sql
CREATE DATABASE tododb;
```

### <a name="create-a-user-with-permissions"></a><span data-ttu-id="930dd-170">Creación de un usuario con permisos</span><span class="sxs-lookup"><span data-stu-id="930dd-170">Create a user with permissions</span></span>

<span data-ttu-id="930dd-171">Cree un usuario de base de datos y concédale todos los privilegios de la base de datos `tododb`.</span><span class="sxs-lookup"><span data-stu-id="930dd-171">Create a database user and give it all privileges in the `tododb` database.</span></span> <span data-ttu-id="930dd-172">Reemplace los marcadores de posición `<Javaapp_user>` y `<Javaapp_password>` por su propio nombre de aplicación único.</span><span class="sxs-lookup"><span data-stu-id="930dd-172">Replace the placeholders `<Javaapp_user>` and `<Javaapp_password>` with your own unique app name.</span></span>

```sql
CREATE USER '<Javaapp_user>' IDENTIFIED BY '<Javaapp_password>'; 
GRANT ALL PRIVILEGES ON tododb.* TO '<Javaapp_user>';
```

<span data-ttu-id="930dd-173">Escriba `quit` para salir de la conexión del servidor.</span><span class="sxs-lookup"><span data-stu-id="930dd-173">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="deploy-the-sample-to-azure-app-service"></a><span data-ttu-id="930dd-174">Implementación de la aplicación en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="930dd-174">Deploy the sample to Azure App Service</span></span>

<span data-ttu-id="930dd-175">Cree un plan de Azure App Service con el plan de tarifa **GRATIS** mediante el comando [az appservice plan create](/cli/azure/appservice/plan#create) de la CLI.</span><span class="sxs-lookup"><span data-stu-id="930dd-175">Create an Azure App Service plan with the **FREE** pricing tier using the  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="930dd-176">Un plan de servicio de aplicaciones define los recursos físicos que se usan para hospedar las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="930dd-176">The appservice plan defines the physical resources used to host your apps.</span></span> <span data-ttu-id="930dd-177">Todas las aplicaciones asignadas a un plan de servicio de aplicaciones comparten los recursos, lo que permite ahorrar costos al hospedar varias aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="930dd-177">All applications assigned to an appservice plan share these resources, allowing you to save cost when hosting multiple apps.</span></span> 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

<span data-ttu-id="930dd-178">Una vez preparado el plan, la CLI de Azure muestra un resultado similar al ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="930dd-178">When the plan is ready, the Azure CLI shows similar output to the following example:</span></span>

```json
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
``` 

### <a name="create-an-azure-web-app"></a><span data-ttu-id="930dd-179">Creación de una aplicación web de Azure</span><span class="sxs-lookup"><span data-stu-id="930dd-179">Create an Azure Web app</span></span>

 <span data-ttu-id="930dd-180">Use el comando de la CLI [az webapp create ](/cli/azure/appservice/web#create) para crear una definición de aplicación web en el plan de App Service `myAppServicePlan`.</span><span class="sxs-lookup"><span data-stu-id="930dd-180">Use the [az webapp create](/cli/azure/appservice/web#create) CLI command to create a web app definition in the `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="930dd-181">La definición de la aplicación web proporciona una dirección URL para acceder a la aplicación y configura varias opciones para implementar el código en Azure.</span><span class="sxs-lookup"><span data-stu-id="930dd-181">The web app definition provides a URL to access your application with and configures several options to deploy your code to Azure.</span></span> 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

<span data-ttu-id="930dd-182">Sustituya el marcador de posición `<app_name>` por su propio nombre de aplicación único.</span><span class="sxs-lookup"><span data-stu-id="930dd-182">Substitute the `<app_name>` placeholder with your own unique app name.</span></span> <span data-ttu-id="930dd-183">Este nombre único forma parte del nombre de dominio predeterminado para la aplicación web, por lo que debe ser único en todas las aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="930dd-183">This unique name is part of the default domain name for the web app, so the name needs to be unique across all apps in Azure.</span></span> <span data-ttu-id="930dd-184">Puede asignar una entrada de nombre de dominio personalizada a la aplicación web antes de exponerla a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="930dd-184">You can map a custom domain name entry to the web app before you expose it to your users.</span></span>

<span data-ttu-id="930dd-185">Cuando está preparada la definición de la aplicación web, la CLI de Azure muestra información similar a la del ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="930dd-185">When the web app definition is ready, the Azure CLI shows information similar to the following example:</span></span> 

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

### <a name="configure-java"></a><span data-ttu-id="930dd-186">Configuración de Java</span><span class="sxs-lookup"><span data-stu-id="930dd-186">Configure Java</span></span> 

<span data-ttu-id="930dd-187">Establezca la configuración del sistema en tiempo de ejecución de Java que necesita la aplicación con el comando [az appservice web config update](/cli/azure/appservice/web/config#update).</span><span class="sxs-lookup"><span data-stu-id="930dd-187">Set up the Java runtime configuration that your app needs with the  [az appservice web config update](/cli/azure/appservice/web/config#update) command.</span></span>

<span data-ttu-id="930dd-188">El siguiente comando configura la aplicación web para que se ejecute en una versión reciente de Java 8 JDK y en [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="930dd-188">The following command configures the web app to run on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

### <a name="configure-the-app-to-use-the-azure-sql-database"></a><span data-ttu-id="930dd-189">Configuración de la aplicación para que use Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="930dd-189">Configure the app to use the Azure SQL database</span></span>

<span data-ttu-id="930dd-190">Antes de ejecutar la aplicación de ejemplo, establezca la configuración de la aplicación en la aplicación web para usar la base de datos MySQL de Azure que creó en Azure.</span><span class="sxs-lookup"><span data-stu-id="930dd-190">Before running the sample app, set application settings on the web app to use the Azure MySQL database you created in Azure.</span></span> <span data-ttu-id="930dd-191">Estas propiedades se exponen a la aplicación web como variables de entorno y reemplazan los valores establecidos en el archivo application.properties dentro de la aplicación web empaquetada.</span><span class="sxs-lookup"><span data-stu-id="930dd-191">These properties are exposed to the web application as environment variables and override the values set in the application.properties inside the packaged web app.</span></span> 

<span data-ttu-id="930dd-192">Establezca la configuración de la aplicación con el parámetro [az webapp config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) en la CLI:</span><span class="sxs-lookup"><span data-stu-id="930dd-192">Set application settings using [az webapp config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) in the CLI:</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_URL="jdbc:mysql://<mysql_server_name>.mysql.database.azure.com:3306/tododb?verifyServerCertificate=true&useSSL=true&requireSSL=false" \
    --resource-group myResourceGroup \
    --name <app_name>
```

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_USERNAME=Javaapp_user@mysql_server_name  \
    --resource-group myResourceGroup \ 
    --name <app_name>
```

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_URL=Javaapp_password \
    --resource-group myResourceGroup \ 
    --name <app_name>
```

### <a name="get-ftp-deployment-credentials"></a><span data-ttu-id="930dd-193">Obtención de credenciales de implementación de FTP</span><span class="sxs-lookup"><span data-stu-id="930dd-193">Get FTP deployment credentials</span></span> 
<span data-ttu-id="930dd-194">Puede implementar la aplicación en el servicio de aplicaciones Azure de diversas formas, incluidos un FTP, un repositorio de Git local, GitHub, Visual Studio Team Services y BitBucket.</span><span class="sxs-lookup"><span data-stu-id="930dd-194">You can deploy your application to Azure appservice in various ways including FTP, local Git, GitHub, Visual Studio Team Services, and BitBucket.</span></span> <span data-ttu-id="930dd-195">En este ejemplo, utilice un comando de FTP para implementar el archivo .WAR creado previamente en el equipo local a Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="930dd-195">For this example, FTP to deploy the .WAR file built previously on your local machine to Azure App Service.</span></span>

<span data-ttu-id="930dd-196">Para determinar qué credenciales pasar a la aplicación web en un comando de FTP, use el comando [az appservice web deployment list-publishing-profiles](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles):</span><span class="sxs-lookup"><span data-stu-id="930dd-196">To determine what credentials to pass along in an ftp command to the Web App, Use [az appservice web deployment list-publishing-profiles](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles) command:</span></span> 

```azurecli-interactive
az webapp deployment list-publishing-profiles \ 
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --query "[?publishMethod=='FTP'].{URL:publishUrl, Username:userName,Password:userPWD}" \ 
    --output json
```

```JSON
[
  {
    "Password": "aBcDeFgHiJkLmNoPqRsTuVwXyZ",
    "URL": "ftp://waws-prod-blu-069.ftp.azurewebsites.windows.net/site/wwwroot",
    "Username": "app_name\\$app_name"
  }
]
```

### <a name="upload-the-app-using-ftp"></a><span data-ttu-id="930dd-197">Carga de la aplicación mediante FTP</span><span class="sxs-lookup"><span data-stu-id="930dd-197">Upload the app using FTP</span></span>

<span data-ttu-id="930dd-198">Utilice la herramienta FTP que prefiera para implementar el archivo .WAR en la carpeta */site/wwwroot/webapps* en la dirección del servidor procedente del campo `URL` en el comando anterior.</span><span class="sxs-lookup"><span data-stu-id="930dd-198">Use your favorite FTP tool to deploy the .WAR file to the */site/wwwroot/webapps* folder on the server address taken from the `URL` field in the previous command.</span></span> <span data-ttu-id="930dd-199">Quite el directorio de aplicación predeterminado (raíz) existente y reemplace el archivo ROOT.war existente con el archivo .WAR creado anteriormente en el tutorial.</span><span class="sxs-lookup"><span data-stu-id="930dd-199">Remove the existing default (ROOT) application directory and replace the existing ROOT.war with the .WAR file built in the earlier in the tutorial.</span></span>

```bash
ftp waws-prod-blu-069.ftp.azurewebsites.windows.net
Connected to waws-prod-blu-069.drip.azurewebsites.windows.net.
220 Microsoft FTP Service
Name (waws-prod-blu-069.ftp.azurewebsites.windows.net:raisa): app_name\$app_name
331 Password required
Password:
cd /site/wwwroot/webapps
mdelete -i ROOT/*
rmdir ROOT/
put target/TodoDemo-0.0.1-SNAPSHOT.war ROOT.war
```

### <a name="test-the-web-app"></a><span data-ttu-id="930dd-200">Prueba de la aplicación web</span><span class="sxs-lookup"><span data-stu-id="930dd-200">Test the web app</span></span>

<span data-ttu-id="930dd-201">Vaya a `http://<app_name>.azurewebsites.net/` y agregue algunas tareas a la lista.</span><span class="sxs-lookup"><span data-stu-id="930dd-201">Browse to `http://<app_name>.azurewebsites.net/` and add a few tasks to the list.</span></span> 

![Aplicación Java que se ejecuta en Azure App Service](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

<span data-ttu-id="930dd-203">**¡Enhorabuena!**</span><span class="sxs-lookup"><span data-stu-id="930dd-203">**Congratulations!**</span></span> <span data-ttu-id="930dd-204">Ya está ejecutando una aplicación Java orientada a datos en Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="930dd-204">You're running a data-driven Java app in Azure App Service.</span></span>

## <a name="update-the-app-and-redeploy"></a><span data-ttu-id="930dd-205">Actualización de la aplicación y nueva implementación</span><span class="sxs-lookup"><span data-stu-id="930dd-205">Update the app and redeploy</span></span>

<span data-ttu-id="930dd-206">Actualice la aplicación para que incluya una columna adicional en la lista de tareas para el día en que se creó el elemento.</span><span class="sxs-lookup"><span data-stu-id="930dd-206">Update the application to include an additional column in the todo list for what day the item was created.</span></span> <span data-ttu-id="930dd-207">Sprint Boot controla la actualización del esquema de base de datos automáticamente cuando cambia el modelo de datos sin modificar los registros de base de datos existente.</span><span class="sxs-lookup"><span data-stu-id="930dd-207">Spring Boot handles updating the database schema for you as the data model changes without altering your existing database records.</span></span>

1. <span data-ttu-id="930dd-208">En el sistema local, abra *src/main/java/com/example/fabrikam/TodoItem.java* y agregue las siguientes importaciones a la clase:</span><span class="sxs-lookup"><span data-stu-id="930dd-208">On your local system, open up *src/main/java/com/example/fabrikam/TodoItem.java* and add the following imports to the class:</span></span>   

    ```java
    import java.text.SimpleDateFormat;
    import java.util.Calendar;
    ```

2. <span data-ttu-id="930dd-209">Agregue una propiedad `String` de `timeCreated` a *src/main/java/com/example/fabrikam/TodoItem.java*, inicializándola con una marca de tiempo en la creación de objeto.</span><span class="sxs-lookup"><span data-stu-id="930dd-209">Add a `String` property `timeCreated` to *src/main/java/com/example/fabrikam/TodoItem.java*, initializing it with a timestamp at object creation.</span></span> <span data-ttu-id="930dd-210">Agregue los métodos captadores/establecedores a la nueva propiedad `timeCreated` mientras edita este archivo.</span><span class="sxs-lookup"><span data-stu-id="930dd-210">Add getters/setters for the new `timeCreated` property while you are editing this file.</span></span>

    ```java
    private String name;
    private boolean complete;
    private String timeCreated;
    ...

    public TodoItem(String category, String name) {
       this.category = category;
       this.name = name;
       this.complete = false;
       this.timeCreated = new SimpleDateFormat("MMMM dd, YYYY").format(Calendar.getInstance().getTime());
    }
    ...
    public void setTimeCreated(String timeCreated) {
       this.timeCreated = timeCreated;
    }

    public String getTimeCreated() {
        return timeCreated;
    }
    ```

3. <span data-ttu-id="930dd-211">Actualice *src/main/java/com/example/fabrikam/TodoDemoController.java* con una línea en el método `updateTodo` para establecer la marca de tiempo:</span><span class="sxs-lookup"><span data-stu-id="930dd-211">Update *src/main/java/com/example/fabrikam/TodoDemoController.java* with a line in the `updateTodo` method to set the timestamp:</span></span>

    ```java
    item.setComplete(requestItem.isComplete());
    item.setId(requestItem.getId());
    item.setTimeCreated(requestItem.getTimeCreated());
    repository.save(item);
    ```

4. <span data-ttu-id="930dd-212">Agregue compatibilidad al nuevo campo de la plantilla Thymeleaf.</span><span class="sxs-lookup"><span data-stu-id="930dd-212">Add support for the new field in the Thymeleaf template.</span></span> <span data-ttu-id="930dd-213">Actualice *src/main/resources/templates/index.html* con un nuevo encabezado de tabla para la marca de tiempo y un nuevo campo para mostrar el valor de la marca de tiempo en cada fila de datos de tabla.</span><span class="sxs-lookup"><span data-stu-id="930dd-213">Update *src/main/resources/templates/index.html* with a new table header for the timestamp, and a new field to display the value of the timestamp in each table data row.</span></span>

    ```html
    <th>Name</th>
    <th>Category</th>
    <th>Time Created</th>
    <th>Complete</th>
    ...
    <td th:text="${item.category}">item_category</td><input type="hidden" th:field="*{todoList[__${i.index}__].category}"/>
    <td th:text="${item.timeCreated}">item_time_created</td><input type="hidden" th:field="*{todoList[__${i.index}__].timeCreated}"/>
    <td><input type="checkbox" th:checked="${item.complete} == true" th:field="*{todoList[__${i.index}__].complete}"/></td>
    ```

5. <span data-ttu-id="930dd-214">Vuelva a generar la aplicación:</span><span class="sxs-lookup"><span data-stu-id="930dd-214">Rebuild the application:</span></span>

    ```bash
    mvnw clean package 
    ```

6. <span data-ttu-id="930dd-215">Utilice la FTP en el archivo .WAR actualizado como antes, quitando el directorio *site/wwwroot/webapps/ROOT* existente y archivo *ROOT.war*, y después cargando el archivo .WAR actualizado como ROOT.war.</span><span class="sxs-lookup"><span data-stu-id="930dd-215">FTP the updated .WAR as before, removing the existing *site/wwwroot/webapps/ROOT* directory and *ROOT.war*, then uploading the updated .WAR file as ROOT.war.</span></span> 

<span data-ttu-id="930dd-216">Al actualizar la aplicación, ahora es visible la columna **Hora de creación**.</span><span class="sxs-lookup"><span data-stu-id="930dd-216">When you refresh the app, a **Time Created** column is now visible.</span></span> <span data-ttu-id="930dd-217">Cuando se agrega una nueva tarea, la aplicación rellenará automáticamente la marca de tiempo.</span><span class="sxs-lookup"><span data-stu-id="930dd-217">When you add a new task, the app will populate the timestamp automatically.</span></span> <span data-ttu-id="930dd-218">Las tareas existentes permanecen sin cambios y trabajan con la aplicación aunque haya cambiado el modelo de datos subyacente.</span><span class="sxs-lookup"><span data-stu-id="930dd-218">Your existing tasks remain unchanged and work with the app even though the underlying data model has changed.</span></span> 

![Aplicación de Java actualizada con una nueva columna](./media/app-service-web-tutorial-java-mysql/appservice-updates-java.png)
      
## <a name="stream-diagnostic-logs"></a><span data-ttu-id="930dd-220">Transmisión de registros de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="930dd-220">Stream diagnostic logs</span></span> 

<span data-ttu-id="930dd-221">Mientras se ejecuta la aplicación Java en Azure App Service, puede tener los registros de consola insertados directamente en el terminal.</span><span class="sxs-lookup"><span data-stu-id="930dd-221">While your Java application runs in Azure App Service, you can get the console logs piped directly to your terminal.</span></span> <span data-ttu-id="930dd-222">De este modo, puede obtener los mismos mensajes de diagnóstico para ayudarle a depurar errores de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="930dd-222">That way, you can get the same diagnostic messages to help you debug application errors.</span></span>

<span data-ttu-id="930dd-223">Para iniciar la transmisión del registro, use el comando [az webapp log tail](/cli/azure/appservice/web/log#tail).</span><span class="sxs-lookup"><span data-stu-id="930dd-223">To start log streaming, use the [az webapp log tail](/cli/azure/appservice/web/log#tail) command.</span></span>

```azurecli-interactive 
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup 
``` 

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="930dd-224">Administración de la aplicación web de Azure</span><span class="sxs-lookup"><span data-stu-id="930dd-224">Manage your Azure web app</span></span>

<span data-ttu-id="930dd-225">Vaya al portal de Azure para ver la aplicación web que ha creado.</span><span class="sxs-lookup"><span data-stu-id="930dd-225">Go to the Azure portal to see the web app you created.</span></span>

<span data-ttu-id="930dd-226">Para ello, inicie sesión en [https://portal.azure.com/](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="930dd-226">To do this, sign in to [https://portal.azure.com](https://portal.azure.com).</span></span>

<span data-ttu-id="930dd-227">En el menú izquierdo, haga clic en **App Service**, a continuación, haga clic en el nombre de la aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="930dd-227">From the left menu, click **App Service**, then click the name of your Azure web app.</span></span>

![Navegación desde el portal a la aplicación web de Azure](./media/app-service-web-tutorial-java-mysql/access-portal.png)

<span data-ttu-id="930dd-229">De forma predeterminada, la hoja de la aplicación web muestra la página de **introducción**.</span><span class="sxs-lookup"><span data-stu-id="930dd-229">By default, your web app's blade shows the **Overview** page.</span></span> <span data-ttu-id="930dd-230">Esta página proporciona una visión del funcionamiento de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="930dd-230">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="930dd-231">En este caso, también puede realizar tareas de administración como detener, iniciar, reiniciar y eliminar.</span><span class="sxs-lookup"><span data-stu-id="930dd-231">Here, you can also perform management tasks like stop, start, restart, and delete.</span></span> <span data-ttu-id="930dd-232">Las pestañas del lado izquierdo de la hoja muestran las diferentes páginas de configuración que puede abrir.</span><span class="sxs-lookup"><span data-stu-id="930dd-232">The tabs on the left side of the blade show the different configuration pages you can open.</span></span>

![Hoja de App Service en Azure Portal](./media/app-service-web-tutorial-java-mysql/web-app-blade.png)

<span data-ttu-id="930dd-234">Estas pestañas de la hoja muestran las muchas y excepcionales características que puede agregar a la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="930dd-234">These tabs in the blade show the many great features you can add to your web app.</span></span> <span data-ttu-id="930dd-235">La lista siguiente proporciona solo algunas de las posibilidades:</span><span class="sxs-lookup"><span data-stu-id="930dd-235">The following list gives you just a few of the possibilities:</span></span>
* <span data-ttu-id="930dd-236">Asignación de un nombre DNS personalizado</span><span class="sxs-lookup"><span data-stu-id="930dd-236">Map a custom DNS name</span></span>
* <span data-ttu-id="930dd-237">Enlace de un certificado SSL personalizado</span><span class="sxs-lookup"><span data-stu-id="930dd-237">Bind a custom SSL certificate</span></span>
* <span data-ttu-id="930dd-238">Configuración de la implementación continua</span><span class="sxs-lookup"><span data-stu-id="930dd-238">Configure continuous deployment</span></span>
* <span data-ttu-id="930dd-239">Escalado vertical y horizontal</span><span class="sxs-lookup"><span data-stu-id="930dd-239">Scale up and out</span></span>
* <span data-ttu-id="930dd-240">Adición de la autenticación de usuarios</span><span class="sxs-lookup"><span data-stu-id="930dd-240">Add user authentication</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="930dd-241">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="930dd-241">Clean up resources</span></span>

<span data-ttu-id="930dd-242">Si no necesita estos recursos para otro tutorial (consulte [Pasos siguientes](#next)), puede ejecutar el siguiente comando para eliminarlos:</span><span class="sxs-lookup"><span data-stu-id="930dd-242">If you don't need these resources for another tutorial (see [Next steps](#next)), you can delete them by running the following command:</span></span> 
  
```azurecli-interactive
az group delete --name myResourceGroup 
``` 

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="930dd-243">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="930dd-243">Next steps</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="930dd-244">Crear una base de datos MySQL en Azure</span><span class="sxs-lookup"><span data-stu-id="930dd-244">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="930dd-245">Conexión de una aplicación Java de ejemplo a MySQL</span><span class="sxs-lookup"><span data-stu-id="930dd-245">Connect a sample Java app to the MySQL</span></span>
> * <span data-ttu-id="930dd-246">Implementación de la aplicación en Azure</span><span class="sxs-lookup"><span data-stu-id="930dd-246">Deploy the app to Azure</span></span>
> * <span data-ttu-id="930dd-247">Actualización de la aplicación y nueva implementación</span><span class="sxs-lookup"><span data-stu-id="930dd-247">Update and redeploy the app</span></span>
> * <span data-ttu-id="930dd-248">Transmitir registros de diagnóstico desde Azure</span><span class="sxs-lookup"><span data-stu-id="930dd-248">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="930dd-249">Administrar la aplicación en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="930dd-249">Manage the app in the Azure portal</span></span>

<span data-ttu-id="930dd-250">Pase al siguiente tutorial para aprender cómo asignar un nombre DNS personalizado a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="930dd-250">Advance to the next tutorial to learn how to map a custom DNS name to the app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="930dd-251">Asignar un nombre DNS personalizado a Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="930dd-251">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)