---
title: "Inicio rápido: Creación de una Base de datos de Azure para el servidor MySQL: CLI de Azure | Microsoft Docs"
description: "En esta guía de inicio rápido se describe cómo usar la CLI de Azure para crear una Base de datos de Azure para el servidor MySQL en un grupo de recursos de Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: hero-article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 04fc441aee7a4c8adc4f02d5e51b2d9e64400f55
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-database-for-mysql-server-using-azure-cli"></a><span data-ttu-id="a3862-103">Creación de una Base de datos de Azure para el servidor MySQL con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="a3862-103">Create an Azure Database for MySQL server using Azure CLI</span></span>
<span data-ttu-id="a3862-104">En esta guía de inicio rápido se describe cómo usar la CLI de Azure para crear una Base de datos de Azure para el servidor MySQL en un grupo de recursos de Azure en unos cinco minutos.</span><span class="sxs-lookup"><span data-stu-id="a3862-104">This quickstart describes how to use the Azure CLI to create an Azure Database for MySQL server in an Azure resource group in about five minutes.</span></span> <span data-ttu-id="a3862-105">La CLI de Azure se usa para crear y administrar recursos de Azure desde la línea de comandos o en scripts.</span><span class="sxs-lookup"><span data-stu-id="a3862-105">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span>

<span data-ttu-id="a3862-106">Si no tiene una suscripción a Azure, cree una cuenta [gratuita](https://azure.microsoft.com/free/) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="a3862-106">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a3862-107">Si decide instalar y usar la CLI localmente, para este tema es preciso que ejecute la CLI de Azure versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="a3862-107">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="a3862-108">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="a3862-108">Run `az --version` to find the version.</span></span> <span data-ttu-id="a3862-109">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a3862-109">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="a3862-110">Si tiene varias suscripciones, elija la adecuada donde se encuentre el recurso o para la cual se facture.</span><span class="sxs-lookup"><span data-stu-id="a3862-110">If you have multiple subscriptions, choose the appropriate subscription in which the resource exists or is billed for.</span></span> <span data-ttu-id="a3862-111">Seleccione un identificador de suscripción específico en su cuenta mediante el comando [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="a3862-111">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="a3862-112">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="a3862-112">Create a resource group</span></span>
<span data-ttu-id="a3862-113">Cree un [grupo de recursos de Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) con el comando [az group create](https://docs.microsoft.com/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="a3862-113">Create an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) using the [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> <span data-ttu-id="a3862-114">Un grupo de recursos es un contenedor lógico en el que se implementan y se administran recursos de Azure como un grupo.</span><span class="sxs-lookup"><span data-stu-id="a3862-114">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span>

<span data-ttu-id="a3862-115">En el ejemplo siguiente, se crea un grupo de recursos denominado `myresourcegroup` en la ubicación `westus`.</span><span class="sxs-lookup"><span data-stu-id="a3862-115">The following example creates a resource group named `myresourcegroup` in the `westus` location.</span></span>

```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="a3862-116">Creación de una Base de datos de Azure para el servidor MySQL</span><span class="sxs-lookup"><span data-stu-id="a3862-116">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="a3862-117">Cree una Base de datos de Azure para el servidor MySQL con el comando **az mysql server create**.</span><span class="sxs-lookup"><span data-stu-id="a3862-117">Create an Azure Database for MySQL server with the **az mysql server create** command.</span></span> <span data-ttu-id="a3862-118">Un servidor puede administrar varias bases de datos.</span><span class="sxs-lookup"><span data-stu-id="a3862-118">A server can manage multiple databases.</span></span> <span data-ttu-id="a3862-119">Normalmente se usa una base de datos independiente para cada proyecto o para cada usuario.</span><span class="sxs-lookup"><span data-stu-id="a3862-119">Typically, a separate database is used for each project or for each user.</span></span>

<span data-ttu-id="a3862-120">En el ejemplo siguiente se crea una Base de datos de Azure para el servidor MySQL situado en `westus` en el grupo de recursos `myresourcegroup` con el nombre `myserver4demo`.</span><span class="sxs-lookup"><span data-stu-id="a3862-120">The following example creates an Azure Database for MySQL server located in `westus` in the resource group `myresourcegroup` with name `myserver4demo`.</span></span> <span data-ttu-id="a3862-121">El servidor tiene un inicio de sesión de administrador con el nombre `myadmin` y la contraseña `Password01!`.</span><span class="sxs-lookup"><span data-stu-id="a3862-121">The server has an administrator log in named `myadmin` and password `Password01!`.</span></span> <span data-ttu-id="a3862-122">El servidor se crea con un nivel de rendimiento **Básico** y **50** unidades de proceso compartidas entre todas las bases de datos en el servidor.</span><span class="sxs-lookup"><span data-stu-id="a3862-122">The server is created with **Basic** performance tier and **50** compute units shared between all the databases in the server.</span></span> <span data-ttu-id="a3862-123">Puede escalar o reducir verticalmente el proceso y el almacenamiento según las necesidades de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a3862-123">You can scale compute and storage up or down depending on the application needs.</span></span>

```azurecli-interactive
az mysql server create --resource-group myresourcegroup --name myserver4demo --location westus --admin-user myadmin --admin-password Password01! --performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a><span data-ttu-id="a3862-124">Configurar la regla de firewall</span><span class="sxs-lookup"><span data-stu-id="a3862-124">Configure firewall rule</span></span>
<span data-ttu-id="a3862-125">Cree una regla de firewall de nivel de servidor de Base de datos de Azure para MySQL con el comando **az mysql server firewall-rule create**.</span><span class="sxs-lookup"><span data-stu-id="a3862-125">Create an Azure Database for MySQL server-level firewall rule using the **az mysql server firewall-rule create** command.</span></span> <span data-ttu-id="a3862-126">Una regla de firewall de nivel de servidor permite que una aplicación externa, como la herramienta de línea de comandos **mysql.exe** o MySQL Workbench, se conecte al servidor a través del firewall del servicio Azure MySQL.</span><span class="sxs-lookup"><span data-stu-id="a3862-126">A server-level firewall rule allows an external application, such as the **mysql.exe** command-line tool or MySQL Workbench to connect to your server through the Azure MySQL service firewall.</span></span> 

<span data-ttu-id="a3862-127">En el ejemplo siguiente se crea una regla de firewall para un intervalo de direcciones predefinidas que, en este ejemplo, es todo el intervalo de direcciones IP posible.</span><span class="sxs-lookup"><span data-stu-id="a3862-127">The following example creates a firewall rule for a predefined address range, which in this example is the entire possible range of IP addresses.</span></span>

```azurecli-interactive
az mysql server firewall-rule create --resource-group myresourcegroup --server myserver4demo --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
## <a name="configure-ssl-settings"></a><span data-ttu-id="a3862-128">Configuración de SSL</span><span class="sxs-lookup"><span data-stu-id="a3862-128">Configure SSL settings</span></span>
<span data-ttu-id="a3862-129">De manera predeterminada, se exigen conexiones SSL entre su servidor y las aplicaciones cliente.</span><span class="sxs-lookup"><span data-stu-id="a3862-129">By default, SSL connections between your server and client applications are enforced.</span></span>  <span data-ttu-id="a3862-130">Esto garantiza la seguridad de los datos "en movimiento" cifrando el flujo de datos que circula por Internet.</span><span class="sxs-lookup"><span data-stu-id="a3862-130">This ensures security of "in-motion" data by encrypting the data stream over the internet.</span></span>  <span data-ttu-id="a3862-131">Para facilitar este inicio rápido, se han deshabilitado las conexiones SSL para su servidor.</span><span class="sxs-lookup"><span data-stu-id="a3862-131">To make this quick start easier, we disable SSL connections for your server.</span></span>  <span data-ttu-id="a3862-132">Esto no se recomienda en servidores de producción.</span><span class="sxs-lookup"><span data-stu-id="a3862-132">This is not recommended for production servers.</span></span>  <span data-ttu-id="a3862-133">Para más información, consulte [Configuración de la conectividad SSL en la aplicación para conectarse de forma segura a Azure Database for MySQL](./howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="a3862-133">For more information, see [Configure SSL connectivity in your application to securely connect to Azure Database for MySQL](./howto-configure-ssl.md).</span></span>

<span data-ttu-id="a3862-134">En el ejemplo siguiente se deshabilita la aplicación de SSL en su servidor MySQL.</span><span class="sxs-lookup"><span data-stu-id="a3862-134">The following example disables enforcing SSL on your MySQL server.</span></span>
 
 ```azurecli-interactive
 az mysql server update --resource-group myresourcegroup --name myserver4demo -g -n --ssl-enforcement Disabled
 ```

## <a name="get-the-connection-information"></a><span data-ttu-id="a3862-135">Obtención de la información de conexión</span><span class="sxs-lookup"><span data-stu-id="a3862-135">Get the connection information</span></span>

<span data-ttu-id="a3862-136">Para conectarse al servidor, debe proporcionar las credenciales de acceso y la información del host.</span><span class="sxs-lookup"><span data-stu-id="a3862-136">To connect to your server, you need to provide host information and access credentials.</span></span>

```azurecli-interactive
az mysql server show --resource-group myresourcegroup --name myserver4demo
```

<span data-ttu-id="a3862-137">El resultado está en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="a3862-137">The result is in JSON format.</span></span> <span data-ttu-id="a3862-138">Tome nota de los valores de **fullyQualifiedDomainName** y **administratorLogin**.</span><span class="sxs-lookup"><span data-stu-id="a3862-138">Make a note of the **fullyQualifiedDomainName** and **administratorLogin**.</span></span>
```json
{
  "administratorLogin": "myadmin",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "myserver4demo.mysql.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.DBforMySQL/servers/myserver4demo",
  "location": "westus",
  "name": "myserver4demo",
  "resourceGroup": "myresourcegroup",
  "sku": {
    "capacity": 50,
    "family": null,
    "name": "MYSQLS2M50",
    "size": null,
    "tier": "Basic"
  },
  "storageMb": 2048,
  "tags": null,
  "type": "Microsoft.DBforMySQL/servers",
  "userVisibleState": "Ready",
  "version": null
}
```

## <a name="connect-to-the-server-using-the-mysqlexe-command-line-tool"></a><span data-ttu-id="a3862-139">Conexión al servidor mediante la herramienta mysql.exe de la línea de comandos</span><span class="sxs-lookup"><span data-stu-id="a3862-139">Connect to the server using the mysql.exe command-line tool</span></span>
<span data-ttu-id="a3862-140">Conéctese al servidor mediante la herramienta **mysql.exe** de la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="a3862-140">Connect to your server using the **mysql.exe** command-line tool.</span></span> <span data-ttu-id="a3862-141">Puede descargarlo desde [aquí](https://dev.mysql.com/downloads/) e instalarlo en su equipo.</span><span class="sxs-lookup"><span data-stu-id="a3862-141">You can download MySQL from [here](https://dev.mysql.com/downloads/) and install it on your computer.</span></span> <span data-ttu-id="a3862-142">En su lugar, también puede hacer clic en el botón **Pruébelo** de los códigos de ejemplo o en el botón `>_` de la barra de herramientas situada en la parte superior derecha de Azure Portal e iniciar **Azure Cloud Shell**.</span><span class="sxs-lookup"><span data-stu-id="a3862-142">Instead you may also click the **Try It** button on code samples, or the  `>_` button from the upper right toolbar in the Azure portal, and launch the **Azure Cloud Shell**.</span></span>

<span data-ttu-id="a3862-143">Escriba los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="a3862-143">Type the next commands:</span></span> 

1. <span data-ttu-id="a3862-144">Conéctese al servidor con la herramienta de la línea de comandos **mysql**:</span><span class="sxs-lookup"><span data-stu-id="a3862-144">Connect to the server using **mysql** command-line tool:</span></span>
```azurecli-interactive
 mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

2. <span data-ttu-id="a3862-145">Ver el estado del servidor:</span><span class="sxs-lookup"><span data-stu-id="a3862-145">View server status:</span></span>
```sql
 mysql> status
```
<span data-ttu-id="a3862-146">Si todo se ha realizado correctamente, la herramienta de la línea de comandos debe mostrar el siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="a3862-146">If everything goes well, the command-line tool should output the following text:</span></span>

```dos
C:\Users\>mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
Enter password: ***********
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 65512
Server version: 5.6.26.0 MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> status
--------------
mysql  Ver 14.14 Distrib 5.6.35, for Win64 (x86_64)

Connection id:          65512
Current database:
Current user:           myadmin@116.230.243.143
SSL:                    Not in use
Using delimiter:        ;
Server version:         5.6.26.0 MySQL Community Server (GPL)
Protocol version:       10
Connection:             myserver4demo.mysql.database.azure.com via TCP/IP
Server characterset:    latin1
Db     characterset:    latin1
Client characterset:    gbk
Conn.  characterset:    gbk
TCP port:               3306
Uptime:                 2 days 9 hours 47 min 20 sec

Threads: 4  Questions: 34833  Slow queries: 2  Opens: 84  Flush tables: 4  Open tables: 1  Queries per second avg: 0.167
--------------

mysql>
```

> [!TIP]
> <span data-ttu-id="a3862-147">Para otros comandos, consulte el [capítulo 4.5.1 del Manual de referencia de MySQL 5.7](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).</span><span class="sxs-lookup"><span data-stu-id="a3862-147">For additional commands, see [MySQL 5.7 Reference Manual - Chapter 4.5.1](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).</span></span>

## <a name="connect-to-the-server-using-the-mysql-workbench-gui-tool"></a><span data-ttu-id="a3862-148">Conexión al servidor con la herramienta MySQL Workbench de la GUI</span><span class="sxs-lookup"><span data-stu-id="a3862-148">Connect to the server using the MySQL Workbench GUI tool</span></span>
1.  <span data-ttu-id="a3862-149">Inicie la aplicación MySQL Workbench en el equipo cliente.</span><span class="sxs-lookup"><span data-stu-id="a3862-149">Launch the MySQL Workbench application on your client computer.</span></span> <span data-ttu-id="a3862-150">Puede descargar e instalar MySQL Workbench desde [aquí](https://dev.mysql.com/downloads/workbench/).</span><span class="sxs-lookup"><span data-stu-id="a3862-150">You can download and install MySQL Workbench from [here](https://dev.mysql.com/downloads/workbench/).</span></span>

2.  <span data-ttu-id="a3862-151">En el cuadro de diálogo **Setup New Connection** (Establecer nueva conexión), escriba la siguiente información en la pestaña **Parámetros**:</span><span class="sxs-lookup"><span data-stu-id="a3862-151">In the **Setup New Connection** dialog box, enter the following information on **Parameters** tab:</span></span>

   ![Configuración de una conexión nueva](./media/quickstart-create-mysql-server-database-using-azure-cli/setup-new-connection.png)

| <span data-ttu-id="a3862-153">**Configuración**</span><span class="sxs-lookup"><span data-stu-id="a3862-153">**Setting**</span></span> | <span data-ttu-id="a3862-154">**Valor sugerido**</span><span class="sxs-lookup"><span data-stu-id="a3862-154">**Suggested Value**</span></span> | <span data-ttu-id="a3862-155">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="a3862-155">**Description**</span></span> |
|---|---|---|
|   <span data-ttu-id="a3862-156">Nombre de la conexión</span><span class="sxs-lookup"><span data-stu-id="a3862-156">Connection Name</span></span> | <span data-ttu-id="a3862-157">Mi conexión</span><span class="sxs-lookup"><span data-stu-id="a3862-157">My Connection</span></span> | <span data-ttu-id="a3862-158">Especifique una etiqueta para esta conexión (puede ser cualquier cosa)</span><span class="sxs-lookup"><span data-stu-id="a3862-158">Specify a label for this connection (this can be anything)</span></span> |
| <span data-ttu-id="a3862-159">Método de conexión</span><span class="sxs-lookup"><span data-stu-id="a3862-159">Connection Method</span></span> | <span data-ttu-id="a3862-160">elija Estándar (TCP/IP)</span><span class="sxs-lookup"><span data-stu-id="a3862-160">choose Standard (TCP/IP)</span></span> | <span data-ttu-id="a3862-161">Use el protocolo TCP/IP para conectarse a Azure Database for MySQL></span><span class="sxs-lookup"><span data-stu-id="a3862-161">Use TCP/IP protocol to connect to Azure Database for MySQL></span></span> |
| <span data-ttu-id="a3862-162">Nombre de host.</span><span class="sxs-lookup"><span data-stu-id="a3862-162">Hostname</span></span> | <span data-ttu-id="a3862-163">myserver4demo.mysql.database.azure.com</span><span class="sxs-lookup"><span data-stu-id="a3862-163">myserver4demo.mysql.database.azure.com</span></span> | <span data-ttu-id="a3862-164">Nombre del servidor que anotó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a3862-164">Server name you previously noted.</span></span> |
| <span data-ttu-id="a3862-165">Port</span><span class="sxs-lookup"><span data-stu-id="a3862-165">Port</span></span> | <span data-ttu-id="a3862-166">3306</span><span class="sxs-lookup"><span data-stu-id="a3862-166">3306</span></span> | <span data-ttu-id="a3862-167">Se usa el puerto predeterminado para MySQL.</span><span class="sxs-lookup"><span data-stu-id="a3862-167">The default port for MySQL is used.</span></span> |
| <span data-ttu-id="a3862-168">Nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="a3862-168">Username</span></span> | myadmin@myserver4demo | <span data-ttu-id="a3862-169">El inicio de sesión de administrador del servidor que anotó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a3862-169">The server admin login you previously noted.</span></span> |
| <span data-ttu-id="a3862-170">Password</span><span class="sxs-lookup"><span data-stu-id="a3862-170">Password</span></span> | **** | <span data-ttu-id="a3862-171">Use la contraseña de la cuenta de administrador que configuró anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a3862-171">Use the admin account password you configured earlier.</span></span> |

<span data-ttu-id="a3862-172">Haga clic en **Probar conexión** para probar si todos los parámetros están configurados correctamente.</span><span class="sxs-lookup"><span data-stu-id="a3862-172">Click **Test Connection** to test if all parameters are correctly configured.</span></span>
<span data-ttu-id="a3862-173">Ahora puede hacer clic en la conexión para conectarse correctamente al servidor.</span><span class="sxs-lookup"><span data-stu-id="a3862-173">Now, you can click the connection to successfully connect to the server.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="a3862-174">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="a3862-174">Clean up resources</span></span>
<span data-ttu-id="a3862-175">Si no necesita estos recursos para otra guía de inicio rápido o tutorial, puede eliminarlos con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a3862-175">If you don't need these resources for another quickstart/tutorial, you can delete them by doing the following command:</span></span> 

```azurecli-interactive
az group delete --name myresourcegroup
```

## <a name="next-steps"></a><span data-ttu-id="a3862-176">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a3862-176">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a3862-177">Diseño de una base de datos MySQL con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="a3862-177">Design a MySQL Database with Azure CLI</span></span>](./tutorial-design-database-using-cli.md)
