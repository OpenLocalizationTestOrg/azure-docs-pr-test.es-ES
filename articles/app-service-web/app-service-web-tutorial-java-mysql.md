---
title: "aaaBuild una aplicación web de Java y MySQL en Azure"
description: "Obtenga información acerca de cómo tooget una aplicación Java que conecta servicio de base de datos de MySQL de Azure toohello trabaja en el servicio de aplicaciones de Azure."
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
ms.openlocfilehash: 0820ee9c2b7bf8fcaa22287c27a7ab848a1c4927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-java-and-mysql-web-app-in-azure"></a><span data-ttu-id="bd046-103">Compilación de una aplicación web Java y MySQL en Azure</span><span class="sxs-lookup"><span data-stu-id="bd046-103">Build a Java and MySQL web app in Azure</span></span>

<span data-ttu-id="bd046-104">Este tutorial muestra cómo toocreate un Java web de aplicación en Azure y conectar tooa base de datos de MySQL.</span><span class="sxs-lookup"><span data-stu-id="bd046-104">This tutorial shows you how toocreate a Java web app in Azure and connect it tooa MySQL database.</span></span> <span data-ttu-id="bd046-105">Cuando haya terminado, tendrá una aplicación [Spring Boot](https://projects.spring.io/spring-boot/) que almacena datos en [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) y que se ejecuta en [Azure App Service Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).</span><span class="sxs-lookup"><span data-stu-id="bd046-105">When you are finished, you will have a [Spring Boot](https://projects.spring.io/spring-boot/) application storing data in [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) running on [Azure App Service Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).</span></span>

![Aplicación Java que se ejecuta en Azure App Service](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

<span data-ttu-id="bd046-107">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="bd046-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bd046-108">Crear una base de datos MySQL en Azure</span><span class="sxs-lookup"><span data-stu-id="bd046-108">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="bd046-109">Conectarse a una base de datos de toohello de aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="bd046-109">Connect a sample app toohello database</span></span>
> * <span data-ttu-id="bd046-110">Implementar Hola aplicación tooAzure</span><span class="sxs-lookup"><span data-stu-id="bd046-110">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="bd046-111">Actualizar y volver a implementar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="bd046-111">Update and redeploy hello app</span></span>
> * <span data-ttu-id="bd046-112">Transmitir registros de diagnóstico desde Azure</span><span class="sxs-lookup"><span data-stu-id="bd046-112">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="bd046-113">Supervisar la aplicación hello en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="bd046-113">Monitor hello app in hello Azure portal</span></span>


## <a name="prerequisites"></a><span data-ttu-id="bd046-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="bd046-114">Prerequisites</span></span>

1. [<span data-ttu-id="bd046-115">Descarga e instalación de Git</span><span class="sxs-lookup"><span data-stu-id="bd046-115">Download and install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="bd046-116">Descargue e instale Hola Java JDK de 7 o superior</span><span class="sxs-lookup"><span data-stu-id="bd046-116">Download and install hello Java 7 JDK or above</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
1. [<span data-ttu-id="bd046-117">Descarga, instalación e inicio de MySQL</span><span class="sxs-lookup"><span data-stu-id="bd046-117">Download, install, and start MySQL</span></span>](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="bd046-118">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="bd046-118">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="bd046-119">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd046-119">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="bd046-120">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="bd046-120">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-local-mysql"></a><span data-ttu-id="bd046-121">Preparación de MySQL local</span><span class="sxs-lookup"><span data-stu-id="bd046-121">Prepare local MySQL</span></span> 

<span data-ttu-id="bd046-122">En este paso, creará una base de datos en un servidor de MySQL local para su uso en pruebas aplicación hello localmente en su equipo.</span><span class="sxs-lookup"><span data-stu-id="bd046-122">In this step, you create a database in a local MySQL server for use in testing hello app locally on your machine.</span></span>

### <a name="connect-toomysql-server"></a><span data-ttu-id="bd046-123">Conecte el servidor de tooMySQL</span><span class="sxs-lookup"><span data-stu-id="bd046-123">Connect tooMySQL server</span></span>

<span data-ttu-id="bd046-124">En una ventana de terminal, conéctese tooyour local MySQL server.</span><span class="sxs-lookup"><span data-stu-id="bd046-124">In a terminal window, connect tooyour local MySQL server.</span></span> <span data-ttu-id="bd046-125">Puede utilizar esta ventana de terminal toorun todos los comandos de hello en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="bd046-125">You can use this terminal window toorun all hello commands in this tutorial.</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="bd046-126">Si se le pide una contraseña, escriba contraseña Hola de hello `root` cuenta.</span><span class="sxs-lookup"><span data-stu-id="bd046-126">If you're prompted for a password, enter hello password for hello `root` account.</span></span> <span data-ttu-id="bd046-127">Si no recuerda su contraseña de la cuenta raíz, consulte [MySQL: cómo tooReset Hola contraseña raíz](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span><span class="sxs-lookup"><span data-stu-id="bd046-127">If you don't remember your root account password, see [MySQL: How tooReset hello Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span></span>

<span data-ttu-id="bd046-128">Si el comando se ejecuta correctamente, significa que el servidor MySQL ya se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="bd046-128">If your command runs successfully, then your MySQL server is already running.</span></span> <span data-ttu-id="bd046-129">Si no es así, asegúrese de que el servidor MySQL local debe iniciarse mediante Hola siguiente [pasos posteriores a la instalación de MySQL](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span><span class="sxs-lookup"><span data-stu-id="bd046-129">If not, make sure that your local MySQL server is started by following hello [MySQL post-installation steps](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span></span>

### <a name="create-a-database"></a><span data-ttu-id="bd046-130">Crear una base de datos</span><span class="sxs-lookup"><span data-stu-id="bd046-130">Create a database</span></span> 

<span data-ttu-id="bd046-131">Hola `mysql` símbolo del sistema, cree una base de datos y una tabla para hello elementos pendientes.</span><span class="sxs-lookup"><span data-stu-id="bd046-131">In hello `mysql` prompt, create a database and a table for hello to-do items.</span></span>

```sql
CREATE DATABASE tododb;
```

<span data-ttu-id="bd046-132">Escriba `quit` para salir de la conexión del servidor.</span><span class="sxs-lookup"><span data-stu-id="bd046-132">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="create-and-run-hello-sample-app"></a><span data-ttu-id="bd046-133">Crear y ejecutar la aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="bd046-133">Create and run hello sample app</span></span> 

<span data-ttu-id="bd046-134">En este paso, clonar aplicación de arranque de primavera de ejemplo, configurar base de datos de MySQL local de toouse hello y ejecútelo en el equipo.</span><span class="sxs-lookup"><span data-stu-id="bd046-134">In this step, you clone sample Spring boot app, configure it toouse hello local MySQL database, and run it on your computer.</span></span> 

### <a name="clone-hello-sample"></a><span data-ttu-id="bd046-135">Ejemplo de Hola de clon</span><span class="sxs-lookup"><span data-stu-id="bd046-135">Clone hello sample</span></span>

<span data-ttu-id="bd046-136">En la ventana de terminal de hello, navegue tooa trabajar repositorio de ejemplo de Hola de directorio y clone.</span><span class="sxs-lookup"><span data-stu-id="bd046-136">In hello terminal window, navigate tooa working directory and clone hello sample repository.</span></span> 

```bash
git clone https://github.com/azure-samples/mysql-spring-boot-todo
```

### <a name="configure-hello-app-toouse-hello-mysql-database"></a><span data-ttu-id="bd046-137">Configurar base de datos de hello aplicación toouse Hola MySQL</span><span class="sxs-lookup"><span data-stu-id="bd046-137">Configure hello app toouse hello MySQL database</span></span>

<span data-ttu-id="bd046-138">Hola de actualización `spring.datasource.password` y el valor de *spring-boot-mysql-todo/src/main/resources/application.properties* con hello misma contraseña raíz utiliza el símbolo del sistema de tooopen Hola MySQL:</span><span class="sxs-lookup"><span data-stu-id="bd046-138">Update hello `spring.datasource.password` and  value in *spring-boot-mysql-todo/src/main/resources/application.properties* with hello same root password used tooopen hello MySQL prompt:</span></span>

```
spring.datasource.password=mysqlpass
```

### <a name="build-and-run-hello-sample"></a><span data-ttu-id="bd046-139">Compilar y ejecutar el ejemplo hello</span><span class="sxs-lookup"><span data-stu-id="bd046-139">Build and run hello sample</span></span>

<span data-ttu-id="bd046-140">Compilar y ejecutar el ejemplo hello utilizando hello Maven contenedor incluido en el repositorio de hello:</span><span class="sxs-lookup"><span data-stu-id="bd046-140">Build and run hello sample using hello Maven wrapper included in hello repo:</span></span>

```bash
cd spring-boot-mysql-todo
mvnw package spring-boot:run
```

<span data-ttu-id="bd046-141">Abra su toosee toohttp://localhost:8080 de explorador en el ejemplo de Hola en acción.</span><span class="sxs-lookup"><span data-stu-id="bd046-141">Open your browser toohttp://localhost:8080 toosee in hello sample in action.</span></span> <span data-ttu-id="bd046-142">Si agrega la lista de tareas de toohello, usar hello SQL siguiente comandos de hello MySQL datos de hello tooview pedir datos almacenados en MySQL.</span><span class="sxs-lookup"><span data-stu-id="bd046-142">As you add tasks toohello list,  use hello following SQL commands in hello MySQL prompt tooview hello data stored in MySQL.</span></span>

```SQL
use testdb;
select * from todo_item;
```

<span data-ttu-id="bd046-143">Detener la aplicación hello pulsando `Ctrl` + `C` Hola terminal.</span><span class="sxs-lookup"><span data-stu-id="bd046-143">Stop hello application by hitting `Ctrl`+`C` in hello terminal.</span></span> 

## <a name="create-an-azure-mysql-database"></a><span data-ttu-id="bd046-144">Creación de una base de datos MySQL de Azure</span><span class="sxs-lookup"><span data-stu-id="bd046-144">Create an Azure MySQL database</span></span>

<span data-ttu-id="bd046-145">En este paso, creará un [base de datos de Azure para MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) instancia mediante hello [CLI de Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="bd046-145">In this step, you create an [Azure Database for MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) instance using hello [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="bd046-146">Configurar toouse de aplicación de ejemplo de Hola esta base de datos más adelante en el tutorial de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd046-146">You configure hello sample application toouse this database later on in hello tutorial.</span></span>

<span data-ttu-id="bd046-147">Hola utilice Azure CLI 2.0 en un recurso de ventana de terminal toocreate Hola necesita toohost la aplicación de Java en el servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="bd046-147">Use hello Azure CLI 2.0 in a terminal window toocreate hello resources needed toohost your Java application in Azure appservice.</span></span> <span data-ttu-id="bd046-148">Inicie sesión en la suscripción de Azure con hello tooyour [inicio de sesión de az](/cli/azure/#login) comando y siga hello en pantalla instrucciones.</span><span class="sxs-lookup"><span data-stu-id="bd046-148">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> 

```azurecli-interactive 
az login 
```   

### <a name="create-a-resource-group"></a><span data-ttu-id="bd046-149">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="bd046-149">Create a resource group</span></span>

<span data-ttu-id="bd046-150">Crear un [grupo de recursos](../azure-resource-manager/resource-group-overview.md) con hello [crear grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="bd046-150">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="bd046-151">Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y administran recursos relacionados como aplicaciones web, bases de datos y cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="bd046-151">An Azure resource group is a logical container where related resources like web apps, databases, and storage accounts are deployed and managed.</span></span> 

<span data-ttu-id="bd046-152">Hello en el ejemplo siguiente se crea un grupo de recursos en la región de Europa del Norte hello:</span><span class="sxs-lookup"><span data-stu-id="bd046-152">hello following example creates a resource group in hello North Europe region:</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "North Europe"
```    

<span data-ttu-id="bd046-153">Puede usar para valores toosee Hola posibles `--location`, usar hello [az de servicio de aplicaciones enumerar ubicaciones](/cli/azure/appservice#list-locations) comando.</span><span class="sxs-lookup"><span data-stu-id="bd046-153">toosee hello possible values you can use for `--location`, use hello [az appservice list-locations](/cli/azure/appservice#list-locations) command.</span></span>

### <a name="create-a-mysql-server"></a><span data-ttu-id="bd046-154">Creación de un servidor MySQL</span><span class="sxs-lookup"><span data-stu-id="bd046-154">Create a MySQL server</span></span>

<span data-ttu-id="bd046-155">Crear un servidor de base de datos de Azure para MySQL (versión preliminar) con hello [crear servidor de mysql az](/cli/azure/mysql/server#create) comando.</span><span class="sxs-lookup"><span data-stu-id="bd046-155">Create a server in Azure Database for MySQL (Preview) with hello [az mysql server create](/cli/azure/mysql/server#create) command.</span></span>    
<span data-ttu-id="bd046-156">Sustituya su propio nombre de servidor único de MySQL donde verá hello `<mysql_server_name>` marcador de posición.</span><span class="sxs-lookup"><span data-stu-id="bd046-156">Substitute your own unique MySQL server name where you see hello `<mysql_server_name>` placeholder.</span></span> <span data-ttu-id="bd046-157">Este nombre forma parte del nombre de host del servidor MySQL, `<mysql_server_name>.mysql.database.azure.com`, por lo que necesita toobe único global.</span><span class="sxs-lookup"><span data-stu-id="bd046-157">This name is part of your MySQL server's hostname, `<mysql_server_name>.mysql.database.azure.com`, so it needs toobe globally unique.</span></span> <span data-ttu-id="bd046-158">Reemplace también `<admin_user>` y `<admin_password>` por sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="bd046-158">Also substitute `<admin_user>` and `<admin_password>` with your own values.</span></span>

```azurecli-interactive
az mysql server create --name <mysql_server_name> \ 
    --resource-group myResourceGroup \ 
    --location "North Europe" \
    --admin-user <admin_user> \ 
    --admin-password <admin_password>
```

<span data-ttu-id="bd046-159">Cuando se crea el servidor de MySQL de hello, Hola CLI de Azure muestra información toohello similar siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bd046-159">When hello MySQL server is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

### <a name="configure-server-firewall"></a><span data-ttu-id="bd046-160">Configuración del firewall del servidor</span><span class="sxs-lookup"><span data-stu-id="bd046-160">Configure server firewall</span></span>

<span data-ttu-id="bd046-161">Cree una regla de firewall para el cliente de MySQL server tooallow conexiones con hello [crear az mysql server regla de firewall](/cli/azure/mysql/server/firewall-rule#create) comando.</span><span class="sxs-lookup"><span data-stu-id="bd046-161">Create a firewall rule for your MySQL server tooallow client connections by using hello [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create) command.</span></span> 

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name>  \ 
    --resource-group myResourceGroup \ 
    --start-ip-address 0.0.0.0 \ 
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="bd046-162">Azure Database for MySQL (versión preliminar) no permite en este momento habilitar conexiones automáticamente desde servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="bd046-162">Azure Database for MySQL (Preview) does not currently automatically enable connections from Azure services.</span></span> <span data-ttu-id="bd046-163">Tal y como se asignan dinámicamente direcciones IP en Azure, es mejor tooenable todas las direcciones IP ahora.</span><span class="sxs-lookup"><span data-stu-id="bd046-163">As IP addresses in Azure are dynamically assigned, it is better tooenable all IP addresses for now.</span></span> <span data-ttu-id="bd046-164">Como servicio de hello continúa su vista previa, se habilitarán los mejores métodos para proteger la base de datos.</span><span class="sxs-lookup"><span data-stu-id="bd046-164">As hello service continues its preview, better methods for securing your database will be enabled.</span></span>

## <a name="configure-hello-azure-mysql-database"></a><span data-ttu-id="bd046-165">Configurar la base de datos de MySQL de Azure de Hola</span><span class="sxs-lookup"><span data-stu-id="bd046-165">Configure hello Azure MySQL database</span></span>

<span data-ttu-id="bd046-166">En la ventana de terminal de hello en el equipo, conéctese toohello MySQL server en Azure.</span><span class="sxs-lookup"><span data-stu-id="bd046-166">In hello terminal window on your computer, connect toohello MySQL server in Azure.</span></span> <span data-ttu-id="bd046-167">Usar valor de Hola que especificó anteriormente por `<admin_user>` y `<mysql_server_name>`.</span><span class="sxs-lookup"><span data-stu-id="bd046-167">Use hello value you specified previously for `<admin_user>` and `<mysql_server_name>`.</span></span>

```bash
mysql -u <admin_user>@<mysql_server_name> -h <mysql_server_name>.mysql.database.azure.com -P 3306 -p
```

### <a name="create-a-database"></a><span data-ttu-id="bd046-168">Crear una base de datos</span><span class="sxs-lookup"><span data-stu-id="bd046-168">Create a database</span></span> 

<span data-ttu-id="bd046-169">Hola `mysql` símbolo del sistema, cree una base de datos y una tabla para hello elementos pendientes.</span><span class="sxs-lookup"><span data-stu-id="bd046-169">In hello `mysql` prompt, create a database and a table for hello to-do items.</span></span>

```sql
CREATE DATABASE tododb;
```

### <a name="create-a-user-with-permissions"></a><span data-ttu-id="bd046-170">Creación de un usuario con permisos</span><span class="sxs-lookup"><span data-stu-id="bd046-170">Create a user with permissions</span></span>

<span data-ttu-id="bd046-171">Crear un usuario de base de datos y conceder a todos los privilegios de hello `tododb` base de datos.</span><span class="sxs-lookup"><span data-stu-id="bd046-171">Create a database user and give it all privileges in hello `tododb` database.</span></span> <span data-ttu-id="bd046-172">Reemplace los marcadores de posición de hello `<Javaapp_user>` y `<Javaapp_password>` con su propio nombre de aplicación único.</span><span class="sxs-lookup"><span data-stu-id="bd046-172">Replace hello placeholders `<Javaapp_user>` and `<Javaapp_password>` with your own unique app name.</span></span>

```sql
CREATE USER '<Javaapp_user>' IDENTIFIED BY '<Javaapp_password>'; 
GRANT ALL PRIVILEGES ON tododb.* too'<Javaapp_user>';
```

<span data-ttu-id="bd046-173">Escriba `quit` para salir de la conexión del servidor.</span><span class="sxs-lookup"><span data-stu-id="bd046-173">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="deploy-hello-sample-tooazure-app-service"></a><span data-ttu-id="bd046-174">Implementar el ejemplo de Hola tooAzure servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="bd046-174">Deploy hello sample tooAzure App Service</span></span>

<span data-ttu-id="bd046-175">Crear un plan de servicio de aplicaciones de Azure con hello **libre** tarifa con hello [Crear plan de servicio de aplicaciones az](/cli/azure/appservice/plan#create) comando de CLI.</span><span class="sxs-lookup"><span data-stu-id="bd046-175">Create an Azure App Service plan with hello **FREE** pricing tier using hello  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="bd046-176">plan de servicio de aplicaciones de Hello define Hola recursos físicos que usa toohost sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="bd046-176">hello appservice plan defines hello physical resources used toohost your apps.</span></span> <span data-ttu-id="bd046-177">Todas las aplicaciones asignadas plan de servicio de aplicaciones de tooan compartan estos recursos, permitiéndole toosave costo al hospedar varias aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="bd046-177">All applications assigned tooan appservice plan share these resources, allowing you toosave cost when hosting multiple apps.</span></span> 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

<span data-ttu-id="bd046-178">Si plan de hello está listo, Hola que CLI de Azure muestra similar salida toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bd046-178">When hello plan is ready, hello Azure CLI shows similar output toohello following example:</span></span>

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

### <a name="create-an-azure-web-app"></a><span data-ttu-id="bd046-179">Creación de una aplicación web de Azure</span><span class="sxs-lookup"><span data-stu-id="bd046-179">Create an Azure Web app</span></span>

 <span data-ttu-id="bd046-180">Hola de uso [crear webapp az](/cli/azure/appservice/web#create) toocreate de comando CLI una definición de aplicación web en hello `myAppServicePlan` plan de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="bd046-180">Use hello [az webapp create](/cli/azure/appservice/web#create) CLI command toocreate a web app definition in hello `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="bd046-181">definición de la aplicación Hello web proporciona una tooaccess de dirección URL a la aplicación con y configura varias toodeploy opciones tooAzure de su código.</span><span class="sxs-lookup"><span data-stu-id="bd046-181">hello web app definition provides a URL tooaccess your application with and configures several options toodeploy your code tooAzure.</span></span> 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

<span data-ttu-id="bd046-182">Hola sustituto `<app_name>` marcador de posición con su propio nombre de aplicación único.</span><span class="sxs-lookup"><span data-stu-id="bd046-182">Substitute hello `<app_name>` placeholder with your own unique app name.</span></span> <span data-ttu-id="bd046-183">Este nombre único forma parte del nombre de dominio predeterminado de hello para la aplicación web de hello, por lo que el nombre de hello necesita toobe único en todas las aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="bd046-183">This unique name is part of hello default domain name for hello web app, so hello name needs toobe unique across all apps in Azure.</span></span> <span data-ttu-id="bd046-184">Puede asignar una aplicación web de dominio personalizado nombre entrada toohello antes de exponer tooyour a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="bd046-184">You can map a custom domain name entry toohello web app before you expose it tooyour users.</span></span>

<span data-ttu-id="bd046-185">Cuando la definición de la aplicación hello web está listo, Hola CLI de Azure muestra información toohello similar siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bd046-185">When hello web app definition is ready, hello Azure CLI shows information similar toohello following example:</span></span> 

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

### <a name="configure-java"></a><span data-ttu-id="bd046-186">Configuración de Java</span><span class="sxs-lookup"><span data-stu-id="bd046-186">Configure Java</span></span> 

<span data-ttu-id="bd046-187">Establecer la configuración de tiempo de ejecución de Java de Hola que necesita la aplicación con hello [actualización de la configuración de az servicio de aplicaciones web](/cli/azure/appservice/web/config#update) comando.</span><span class="sxs-lookup"><span data-stu-id="bd046-187">Set up hello Java runtime configuration that your app needs with hello  [az appservice web config update](/cli/azure/appservice/web/config#update) command.</span></span>

<span data-ttu-id="bd046-188">Hello siguiente comando configura toorun de aplicación web de hello en una versión reciente de Java 8 JDK y [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="bd046-188">hello following command configures hello web app toorun on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

### <a name="configure-hello-app-toouse-hello-azure-sql-database"></a><span data-ttu-id="bd046-189">Configurar base de datos de hello aplicación toouse Hola SQL Azure</span><span class="sxs-lookup"><span data-stu-id="bd046-189">Configure hello app toouse hello Azure SQL database</span></span>

<span data-ttu-id="bd046-190">Antes de ejecutar la aplicación de ejemplo de Hola, establecer configuración de la aplicación en hello web app toouse hello Azure base de datos MySQL que creó en Azure.</span><span class="sxs-lookup"><span data-stu-id="bd046-190">Before running hello sample app, set application settings on hello web app toouse hello Azure MySQL database you created in Azure.</span></span> <span data-ttu-id="bd046-191">Estas propiedades son de la aplicación web toohello expuesto como variables de entorno e invalidan los valores de hello establecidos en hello application.properties dentro de la aplicación web empaquetada de hello.</span><span class="sxs-lookup"><span data-stu-id="bd046-191">These properties are exposed toohello web application as environment variables and override hello values set in hello application.properties inside hello packaged web app.</span></span> 

<span data-ttu-id="bd046-192">Establecer la configuración de la aplicación [az webapp configuración appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) Hola CLI:</span><span class="sxs-lookup"><span data-stu-id="bd046-192">Set application settings using [az webapp config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) in hello CLI:</span></span>

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

### <a name="get-ftp-deployment-credentials"></a><span data-ttu-id="bd046-193">Obtención de credenciales de implementación de FTP</span><span class="sxs-lookup"><span data-stu-id="bd046-193">Get FTP deployment credentials</span></span> 
<span data-ttu-id="bd046-194">Puede implementar el servicio de aplicaciones de tooAzure de aplicación de varias maneras, como FTP, local Git, GitHub, Visual Studio Team Services y BitBucket.</span><span class="sxs-lookup"><span data-stu-id="bd046-194">You can deploy your application tooAzure appservice in various ways including FTP, local Git, GitHub, Visual Studio Team Services, and BitBucket.</span></span> <span data-ttu-id="bd046-195">En este ejemplo, FTP toodeploy Hola. Archivo WAR generado anteriormente en el servicio de aplicaciones tooAzure de equipo local.</span><span class="sxs-lookup"><span data-stu-id="bd046-195">For this example, FTP toodeploy hello .WAR file built previously on your local machine tooAzure App Service.</span></span>

<span data-ttu-id="bd046-196">toodetermine sobre qué credenciales se toopass a lo largo de un toohello de comandos de ftp aplicación Web, Use [az servicio de aplicaciones web implementación lista publicación perfiles-](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles) comando:</span><span class="sxs-lookup"><span data-stu-id="bd046-196">toodetermine what credentials toopass along in an ftp command toohello Web App, Use [az appservice web deployment list-publishing-profiles](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles) command:</span></span> 

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

### <a name="upload-hello-app-using-ftp"></a><span data-ttu-id="bd046-197">Cargar la aplicación hello mediante FTP</span><span class="sxs-lookup"><span data-stu-id="bd046-197">Upload hello app using FTP</span></span>

<span data-ttu-id="bd046-198">Utilice los favoritos Hola de toodeploy de herramienta FTP. Toohello de archivo WAR */site/wwwroot/webapps* carpeta en la dirección del servidor hello tomado de Hola `URL` campo comando anterior Hola.</span><span class="sxs-lookup"><span data-stu-id="bd046-198">Use your favorite FTP tool toodeploy hello .WAR file toohello */site/wwwroot/webapps* folder on hello server address taken from hello `URL` field in hello previous command.</span></span> <span data-ttu-id="bd046-199">Quitar el directorio de aplicación predeterminado (raíz) existente hello y reemplace Hola existente ROOT.war con hello. Archivo WAR integrado Hola anteriormente en el tutorial de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd046-199">Remove hello existing default (ROOT) application directory and replace hello existing ROOT.war with hello .WAR file built in hello earlier in hello tutorial.</span></span>

```bash
ftp waws-prod-blu-069.ftp.azurewebsites.windows.net
Connected toowaws-prod-blu-069.drip.azurewebsites.windows.net.
220 Microsoft FTP Service
Name (waws-prod-blu-069.ftp.azurewebsites.windows.net:raisa): app_name\$app_name
331 Password required
Password:
cd /site/wwwroot/webapps
mdelete -i ROOT/*
rmdir ROOT/
put target/TodoDemo-0.0.1-SNAPSHOT.war ROOT.war
```

### <a name="test-hello-web-app"></a><span data-ttu-id="bd046-200">Aplicación de prueba hello web</span><span class="sxs-lookup"><span data-stu-id="bd046-200">Test hello web app</span></span>

<span data-ttu-id="bd046-201">Examinar demasiado`http://<app_name>.azurewebsites.net/` y agregar algunas tareas toohello lista.</span><span class="sxs-lookup"><span data-stu-id="bd046-201">Browse too`http://<app_name>.azurewebsites.net/` and add a few tasks toohello list.</span></span> 

![Aplicación Java que se ejecuta en Azure App Service](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

<span data-ttu-id="bd046-203">**¡Enhorabuena!**</span><span class="sxs-lookup"><span data-stu-id="bd046-203">**Congratulations!**</span></span> <span data-ttu-id="bd046-204">Ya está ejecutando una aplicación Java orientada a datos en Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="bd046-204">You're running a data-driven Java app in Azure App Service.</span></span>

## <a name="update-hello-app-and-redeploy"></a><span data-ttu-id="bd046-205">Volver a implementar y aplicación de hello de actualización</span><span class="sxs-lookup"><span data-stu-id="bd046-205">Update hello app and redeploy</span></span>

<span data-ttu-id="bd046-206">Actualizar Hola aplicación tooinclude una columna adicional en la lista de tareas de Hola para que se creó el elemento de hello día.</span><span class="sxs-lookup"><span data-stu-id="bd046-206">Update hello application tooinclude an additional column in hello todo list for what day hello item was created.</span></span> <span data-ttu-id="bd046-207">Arranque de primavera controla actualizar esquema de base de datos de Hola de como Hola cambios del modelo de datos sin modificar los registros de base de datos existente.</span><span class="sxs-lookup"><span data-stu-id="bd046-207">Spring Boot handles updating hello database schema for you as hello data model changes without altering your existing database records.</span></span>

1. <span data-ttu-id="bd046-208">En el sistema local, se abrirán *src/main/java/com/example/fabrikam/TodoItem.java* y agregue la siguiente Hola importa toohello clase:</span><span class="sxs-lookup"><span data-stu-id="bd046-208">On your local system, open up *src/main/java/com/example/fabrikam/TodoItem.java* and add hello following imports toohello class:</span></span>   

    ```java
    import java.text.SimpleDateFormat;
    import java.util.Calendar;
    ```

2. <span data-ttu-id="bd046-209">Agregar un `String` propiedad `timeCreated` demasiado*src/main/java/com/example/fabrikam/TodoItem.java*, inicializándola con una marca de tiempo en la creación del objeto.</span><span class="sxs-lookup"><span data-stu-id="bd046-209">Add a `String` property `timeCreated` too*src/main/java/com/example/fabrikam/TodoItem.java*, initializing it with a timestamp at object creation.</span></span> <span data-ttu-id="bd046-210">Agregar los captadores/establecedores de hello nueva `timeCreated` propiedad mientras se está editando este archivo.</span><span class="sxs-lookup"><span data-stu-id="bd046-210">Add getters/setters for hello new `timeCreated` property while you are editing this file.</span></span>

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

3. <span data-ttu-id="bd046-211">Actualización *src/main/java/com/example/fabrikam/TodoDemoController.java* con una línea en hello `updateTodo` método tooset Hola timestamp:</span><span class="sxs-lookup"><span data-stu-id="bd046-211">Update *src/main/java/com/example/fabrikam/TodoDemoController.java* with a line in hello `updateTodo` method tooset hello timestamp:</span></span>

    ```java
    item.setComplete(requestItem.isComplete());
    item.setId(requestItem.getId());
    item.setTimeCreated(requestItem.getTimeCreated());
    repository.save(item);
    ```

4. <span data-ttu-id="bd046-212">Agregar compatibilidad para el nuevo campo de hello en plantilla de hello Thymeleaf.</span><span class="sxs-lookup"><span data-stu-id="bd046-212">Add support for hello new field in hello Thymeleaf template.</span></span> <span data-ttu-id="bd046-213">Actualización *src/main/resources/templates/index.html* con un nuevo encabezado de tabla para la marca de tiempo de Hola y un nuevo valor del campo toodisplay Hola de marca de tiempo de hello en cada fila de datos de tabla.</span><span class="sxs-lookup"><span data-stu-id="bd046-213">Update *src/main/resources/templates/index.html* with a new table header for hello timestamp, and a new field toodisplay hello value of hello timestamp in each table data row.</span></span>

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

5. <span data-ttu-id="bd046-214">Recompilar la aplicación hello:</span><span class="sxs-lookup"><span data-stu-id="bd046-214">Rebuild hello application:</span></span>

    ```bash
    mvnw clean package 
    ```

6. <span data-ttu-id="bd046-215">Hola FTP que se actualiza. WAR como antes, quitar Hola existente *sitio/wwwroot/aplicaciones Web/ROOT* directorio y *ROOT.war*, a continuación, cargar Hola actualizado. Archivo WAR como ROOT.war.</span><span class="sxs-lookup"><span data-stu-id="bd046-215">FTP hello updated .WAR as before, removing hello existing *site/wwwroot/webapps/ROOT* directory and *ROOT.war*, then uploading hello updated .WAR file as ROOT.war.</span></span> 

<span data-ttu-id="bd046-216">Al actualizar la aplicación hello, un **vez crea** columna es visible ahora.</span><span class="sxs-lookup"><span data-stu-id="bd046-216">When you refresh hello app, a **Time Created** column is now visible.</span></span> <span data-ttu-id="bd046-217">Cuando se agrega una nueva tarea, aplicación hello rellenará automáticamente Hola marca de tiempo.</span><span class="sxs-lookup"><span data-stu-id="bd046-217">When you add a new task, hello app will populate hello timestamp automatically.</span></span> <span data-ttu-id="bd046-218">Las tareas existentes permanecen sin cambios y trabajar con la aplicación hello aunque Hola subyacente modelo de datos ha cambiado.</span><span class="sxs-lookup"><span data-stu-id="bd046-218">Your existing tasks remain unchanged and work with hello app even though hello underlying data model has changed.</span></span> 

![Aplicación de Java actualizada con una nueva columna](./media/app-service-web-tutorial-java-mysql/appservice-updates-java.png)
      
## <a name="stream-diagnostic-logs"></a><span data-ttu-id="bd046-220">Transmisión de registros de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="bd046-220">Stream diagnostic logs</span></span> 

<span data-ttu-id="bd046-221">Mientras se ejecuta la aplicación de Java en el servicio de aplicación de Azure, puede obtener consola Hola registros directamente canalizan tooyour terminal.</span><span class="sxs-lookup"><span data-stu-id="bd046-221">While your Java application runs in Azure App Service, you can get hello console logs piped directly tooyour terminal.</span></span> <span data-ttu-id="bd046-222">De este modo, puede obtener Hola mensajes de diagnóstico del mismo toohelp depurar errores de aplicación.</span><span class="sxs-lookup"><span data-stu-id="bd046-222">That way, you can get hello same diagnostic messages toohelp you debug application errors.</span></span>

<span data-ttu-id="bd046-223">registro toostart transmisión por secuencias, utilice hello [final del registro de aplicación Web az](/cli/azure/appservice/web/log#tail) comando.</span><span class="sxs-lookup"><span data-stu-id="bd046-223">toostart log streaming, use hello [az webapp log tail](/cli/azure/appservice/web/log#tail) command.</span></span>

```azurecli-interactive 
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup 
``` 

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="bd046-224">Administración de la aplicación web de Azure</span><span class="sxs-lookup"><span data-stu-id="bd046-224">Manage your Azure web app</span></span>

<span data-ttu-id="bd046-225">Vaya toohello toosee portal Azure hello web aplicación que creó.</span><span class="sxs-lookup"><span data-stu-id="bd046-225">Go toohello Azure portal toosee hello web app you created.</span></span>

<span data-ttu-id="bd046-226">toodo esto, inicie sesión en demasiado[https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bd046-226">toodo this, sign in too[https://portal.azure.com](https://portal.azure.com).</span></span>

<span data-ttu-id="bd046-227">Hola menú izquierdo, haga clic en **servicio de aplicaciones**, a continuación, haga clic en nombre de saludo de la aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="bd046-227">From hello left menu, click **App Service**, then click hello name of your Azure web app.</span></span>

![Aplicación de navegación del portal tooAzure web](./media/app-service-web-tutorial-java-mysql/access-portal.png)

<span data-ttu-id="bd046-229">De forma predeterminada, la hoja de la aplicación web muestra hello **Introducción** página.</span><span class="sxs-lookup"><span data-stu-id="bd046-229">By default, your web app's blade shows hello **Overview** page.</span></span> <span data-ttu-id="bd046-230">Esta página proporciona una visión del funcionamiento de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bd046-230">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="bd046-231">En este caso, también puede realizar tareas de administración como detener, iniciar, reiniciar y eliminar.</span><span class="sxs-lookup"><span data-stu-id="bd046-231">Here, you can also perform management tasks like stop, start, restart, and delete.</span></span> <span data-ttu-id="bd046-232">pestañas: Hola a la izquierda Hola de hoja de hello páginas de configuración diferente de hello que puede abrir.</span><span class="sxs-lookup"><span data-stu-id="bd046-232">hello tabs on hello left side of hello blade show hello different configuration pages you can open.</span></span>

![Hoja de App Service en Azure Portal](./media/app-service-web-tutorial-java-mysql/web-app-blade.png)

<span data-ttu-id="bd046-234">Estas pestañas de hoja de hello mostrarán hello muchas características excepcionales, puede agregar la aplicación web de tooyour.</span><span class="sxs-lookup"><span data-stu-id="bd046-234">These tabs in hello blade show hello many great features you can add tooyour web app.</span></span> <span data-ttu-id="bd046-235">Hola lista siguiente proporciona solo algunas de las posibilidades de hello:</span><span class="sxs-lookup"><span data-stu-id="bd046-235">hello following list gives you just a few of hello possibilities:</span></span>
* <span data-ttu-id="bd046-236">Asignación de un nombre DNS personalizado</span><span class="sxs-lookup"><span data-stu-id="bd046-236">Map a custom DNS name</span></span>
* <span data-ttu-id="bd046-237">Enlace de un certificado SSL personalizado</span><span class="sxs-lookup"><span data-stu-id="bd046-237">Bind a custom SSL certificate</span></span>
* <span data-ttu-id="bd046-238">Configuración de la implementación continua</span><span class="sxs-lookup"><span data-stu-id="bd046-238">Configure continuous deployment</span></span>
* <span data-ttu-id="bd046-239">Escalado vertical y horizontal</span><span class="sxs-lookup"><span data-stu-id="bd046-239">Scale up and out</span></span>
* <span data-ttu-id="bd046-240">Adición de la autenticación de usuarios</span><span class="sxs-lookup"><span data-stu-id="bd046-240">Add user authentication</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="bd046-241">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="bd046-241">Clean up resources</span></span>

<span data-ttu-id="bd046-242">Si no necesita estos recursos para otro tutorial (vea [pasos siguientes](#next)), puede eliminarlos mediante la ejecución de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="bd046-242">If you don't need these resources for another tutorial (see [Next steps](#next)), you can delete them by running hello following command:</span></span> 
  
```azurecli-interactive
az group delete --name myResourceGroup 
``` 

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="bd046-243">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bd046-243">Next steps</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bd046-244">Crear una base de datos MySQL en Azure</span><span class="sxs-lookup"><span data-stu-id="bd046-244">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="bd046-245">Conectar una aplicación de Java ejemplo toohello MySQL</span><span class="sxs-lookup"><span data-stu-id="bd046-245">Connect a sample Java app toohello MySQL</span></span>
> * <span data-ttu-id="bd046-246">Implementar Hola aplicación tooAzure</span><span class="sxs-lookup"><span data-stu-id="bd046-246">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="bd046-247">Actualizar y volver a implementar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="bd046-247">Update and redeploy hello app</span></span>
> * <span data-ttu-id="bd046-248">Transmitir registros de diagnóstico desde Azure</span><span class="sxs-lookup"><span data-stu-id="bd046-248">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="bd046-249">Administrar aplicación Hola Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="bd046-249">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="bd046-250">Avanzar toohello siguiente tutorial toolearn cómo toomap un DNS personalizado nombre toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="bd046-250">Advance toohello next tutorial toolearn how toomap a custom DNS name toohello app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="bd046-251">Asignar un tooAzure de nombre DNS personalizado existente aplicaciones Web</span><span class="sxs-lookup"><span data-stu-id="bd046-251">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
