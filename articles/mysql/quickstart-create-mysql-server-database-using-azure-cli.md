---
title: "Inicio rápido: Creación de una Base de datos de Azure para el servidor MySQL: CLI de Azure | Microsoft Docs"
description: "Este tutorial describe cómo toouse Hola toocreate de CLI de Azure a una base de datos de Azure para servidor de MySQL en un grupo de recursos de Azure."
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
ms.openlocfilehash: 708d0cce12e812cb464adcf7e83e6f85c196bafe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-mysql-server-using-azure-cli"></a><span data-ttu-id="2722c-103">Creación de una Base de datos de Azure para el servidor MySQL con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="2722c-103">Create an Azure Database for MySQL server using Azure CLI</span></span>
<span data-ttu-id="2722c-104">Este tutorial describe cómo toouse Hola CLI de Azure toocreate una base de datos de Azure para servidor de MySQL en un grupo de recursos de Azure en aproximadamente cinco minutos.</span><span class="sxs-lookup"><span data-stu-id="2722c-104">This quickstart describes how toouse hello Azure CLI toocreate an Azure Database for MySQL server in an Azure resource group in about five minutes.</span></span> <span data-ttu-id="2722c-105">Hola CLI de Azure es toocreate usado y administrar recursos de Azure desde la línea de comandos de Hola o en scripts.</span><span class="sxs-lookup"><span data-stu-id="2722c-105">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span>

<span data-ttu-id="2722c-106">Si no tiene una suscripción a Azure, cree una cuenta [gratuita](https://azure.microsoft.com/free/) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="2722c-106">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="2722c-107">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="2722c-107">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="2722c-108">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="2722c-108">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="2722c-109">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2722c-109">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="2722c-110">Si tiene varias suscripciones, elija Hola de suscripción adecuado en el que recurso de hello existe o se factura para.</span><span class="sxs-lookup"><span data-stu-id="2722c-110">If you have multiple subscriptions, choose hello appropriate subscription in which hello resource exists or is billed for.</span></span> <span data-ttu-id="2722c-111">Seleccione un identificador de suscripción específico en su cuenta mediante el comando [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="2722c-111">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="2722c-112">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="2722c-112">Create a resource group</span></span>
<span data-ttu-id="2722c-113">Crear un [grupo de recursos de Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) con hello [crear grupo az](https://docs.microsoft.com/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="2722c-113">Create an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) using hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> <span data-ttu-id="2722c-114">Un grupo de recursos es un contenedor lógico en el que se implementan y se administran recursos de Azure como un grupo.</span><span class="sxs-lookup"><span data-stu-id="2722c-114">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span>

<span data-ttu-id="2722c-115">Hello en el ejemplo siguiente se crea un grupo de recursos denominado `myresourcegroup` en hello `westus` ubicación.</span><span class="sxs-lookup"><span data-stu-id="2722c-115">hello following example creates a resource group named `myresourcegroup` in hello `westus` location.</span></span>

```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="2722c-116">Creación de un servidor de Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="2722c-116">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="2722c-117">Crear una base de datos de Azure para servidor de MySQL con hello **crear servidor de mysql az** comando.</span><span class="sxs-lookup"><span data-stu-id="2722c-117">Create an Azure Database for MySQL server with hello **az mysql server create** command.</span></span> <span data-ttu-id="2722c-118">Un servidor puede administrar varias bases de datos.</span><span class="sxs-lookup"><span data-stu-id="2722c-118">A server can manage multiple databases.</span></span> <span data-ttu-id="2722c-119">Normalmente se usa una base de datos independiente para cada proyecto o para cada usuario.</span><span class="sxs-lookup"><span data-stu-id="2722c-119">Typically, a separate database is used for each project or for each user.</span></span>

<span data-ttu-id="2722c-120">Hello en el ejemplo siguiente se crea una base de datos de Azure para MySQL server que se encuentra en `westus` en grupo de recursos de hello `myresourcegroup` con nombre `myserver4demo`.</span><span class="sxs-lookup"><span data-stu-id="2722c-120">hello following example creates an Azure Database for MySQL server located in `westus` in hello resource group `myresourcegroup` with name `myserver4demo`.</span></span> <span data-ttu-id="2722c-121">servidor de Hello tiene un inicio de sesión de administrador en denominado `myadmin` y la contraseña `Password01!`.</span><span class="sxs-lookup"><span data-stu-id="2722c-121">hello server has an administrator log in named `myadmin` and password `Password01!`.</span></span> <span data-ttu-id="2722c-122">Hola servidor se crea con **básica** nivel de rendimiento y **50** unidades que se comparten entre todas las bases de datos de hello en el servidor de Hola de proceso.</span><span class="sxs-lookup"><span data-stu-id="2722c-122">hello server is created with **Basic** performance tier and **50** compute units shared between all hello databases in hello server.</span></span> <span data-ttu-id="2722c-123">Puede escalar almacenamiento y el proceso hacia arriba o hacia abajo según las necesidades de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="2722c-123">You can scale compute and storage up or down depending on hello application needs.</span></span>

```azurecli-interactive
az mysql server create --resource-group myresourcegroup --name myserver4demo --location westus --admin-user myadmin --admin-password Password01! --performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a><span data-ttu-id="2722c-124">Configurar de la regla de firewall</span><span class="sxs-lookup"><span data-stu-id="2722c-124">Configure firewall rule</span></span>
<span data-ttu-id="2722c-125">Crear una base de datos de Azure para la regla de firewall de nivel de servidor de MySQL mediante hello **crear az mysql server regla de firewall** comando.</span><span class="sxs-lookup"><span data-stu-id="2722c-125">Create an Azure Database for MySQL server-level firewall rule using hello **az mysql server firewall-rule create** command.</span></span> <span data-ttu-id="2722c-126">Una regla de firewall de nivel de servidor permite que una aplicación externa, por ejemplo, hello **mysql.exe** herramienta de línea de comandos o servidor de MySQL Workbench tooconnect tooyour a través de firewall de servicio de MySQL de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="2722c-126">A server-level firewall rule allows an external application, such as hello **mysql.exe** command-line tool or MySQL Workbench tooconnect tooyour server through hello Azure MySQL service firewall.</span></span> 

<span data-ttu-id="2722c-127">Hello en el ejemplo siguiente se crea una regla de firewall para un intervalo de direcciones predefinidos, que en este ejemplo es Hola todo posible intervalo de direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="2722c-127">hello following example creates a firewall rule for a predefined address range, which in this example is hello entire possible range of IP addresses.</span></span>

```azurecli-interactive
az mysql server firewall-rule create --resource-group myresourcegroup --server myserver4demo --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
## <a name="configure-ssl-settings"></a><span data-ttu-id="2722c-128">Configuración de SSL</span><span class="sxs-lookup"><span data-stu-id="2722c-128">Configure SSL settings</span></span>
<span data-ttu-id="2722c-129">De manera predeterminada, se exigen conexiones SSL entre su servidor y las aplicaciones cliente.</span><span class="sxs-lookup"><span data-stu-id="2722c-129">By default, SSL connections between your server and client applications are enforced.</span></span>  <span data-ttu-id="2722c-130">Esto garantiza la seguridad de "en movimiento" Hola a datos mediante el cifrado de flujo de datos de hello en internet.</span><span class="sxs-lookup"><span data-stu-id="2722c-130">This ensures security of "in-motion" data by encrypting hello data stream over hello internet.</span></span>  <span data-ttu-id="2722c-131">toomake más fácil de inicio de este rápido, se deshabilita las conexiones SSL para el servidor.</span><span class="sxs-lookup"><span data-stu-id="2722c-131">toomake this quick start easier, we disable SSL connections for your server.</span></span>  <span data-ttu-id="2722c-132">Esto no se recomienda en servidores de producción.</span><span class="sxs-lookup"><span data-stu-id="2722c-132">This is not recommended for production servers.</span></span>  <span data-ttu-id="2722c-133">Para obtener más información, consulte [tooAzure base de datos de conexión de conectividad de configurar SSL en su aplicación toosecurely para MySQL](./howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="2722c-133">For more information, see [Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL](./howto-configure-ssl.md).</span></span>

<span data-ttu-id="2722c-134">Hello en el ejemplo siguiente se deshabilita la implantación SSL en el servidor MySQL.</span><span class="sxs-lookup"><span data-stu-id="2722c-134">hello following example disables enforcing SSL on your MySQL server.</span></span>
 
 ```azurecli-interactive
 az mysql server update --resource-group myresourcegroup --name myserver4demo -g -n --ssl-enforcement Disabled
 ```

## <a name="get-hello-connection-information"></a><span data-ttu-id="2722c-135">Obtener información de conexión de Hola</span><span class="sxs-lookup"><span data-stu-id="2722c-135">Get hello connection information</span></span>

<span data-ttu-id="2722c-136">tooconnect tooyour server, necesita credenciales de acceso y la información de host de tooprovide.</span><span class="sxs-lookup"><span data-stu-id="2722c-136">tooconnect tooyour server, you need tooprovide host information and access credentials.</span></span>

```azurecli-interactive
az mysql server show --resource-group myresourcegroup --name myserver4demo
```

<span data-ttu-id="2722c-137">resultado de Hello es en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="2722c-137">hello result is in JSON format.</span></span> <span data-ttu-id="2722c-138">Tome nota de hello **fullyQualifiedDomainName** y **Iniciodesesióndeadministrador**.</span><span class="sxs-lookup"><span data-stu-id="2722c-138">Make a note of hello **fullyQualifiedDomainName** and **administratorLogin**.</span></span>
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

## <a name="connect-toohello-server-using-hello-mysqlexe-command-line-tool"></a><span data-ttu-id="2722c-139">Conectar servidor toohello mediante la herramienta de línea de comandos de hello mysql.exe</span><span class="sxs-lookup"><span data-stu-id="2722c-139">Connect toohello server using hello mysql.exe command-line tool</span></span>
<span data-ttu-id="2722c-140">Conectar servidor tooyour con hello **mysql.exe** herramienta de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="2722c-140">Connect tooyour server using hello **mysql.exe** command-line tool.</span></span> <span data-ttu-id="2722c-141">Puede descargarlo desde [aquí](https://dev.mysql.com/downloads/) e instalarlo en su equipo.</span><span class="sxs-lookup"><span data-stu-id="2722c-141">You can download MySQL from [here](https://dev.mysql.com/downloads/) and install it on your computer.</span></span> <span data-ttu-id="2722c-142">En su lugar, también puede hacer clic en hello **inténtelo** situado en ejemplos de código u Hola `>_` botón de hello superior derecho barra de herramientas de hello portal de Azure y lanzamiento hello **Shell en la nube de Azure**.</span><span class="sxs-lookup"><span data-stu-id="2722c-142">Instead you may also click hello **Try It** button on code samples, or hello  `>_` button from hello upper right toolbar in hello Azure portal, and launch hello **Azure Cloud Shell**.</span></span>

<span data-ttu-id="2722c-143">Escriba Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="2722c-143">Type hello next commands:</span></span> 

1. <span data-ttu-id="2722c-144">Conectar con servidor de toohello **mysql** herramienta de línea de comandos:</span><span class="sxs-lookup"><span data-stu-id="2722c-144">Connect toohello server using **mysql** command-line tool:</span></span>
```azurecli-interactive
 mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

2. <span data-ttu-id="2722c-145">Ver el estado del servidor:</span><span class="sxs-lookup"><span data-stu-id="2722c-145">View server status:</span></span>
```sql
 mysql> status
```
<span data-ttu-id="2722c-146">Si todo va bien, herramienta de línea de comandos de hello debe devolver Hola siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="2722c-146">If everything goes well, hello command-line tool should output hello following text:</span></span>

```dos
C:\Users\>mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
Enter password: ***********
Welcome toohello MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 65512
Server version: 5.6.26.0 MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' tooclear hello current input statement.

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
> <span data-ttu-id="2722c-147">Para otros comandos, consulte el [capítulo 4.5.1 del Manual de referencia de MySQL 5.7](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).</span><span class="sxs-lookup"><span data-stu-id="2722c-147">For additional commands, see [MySQL 5.7 Reference Manual - Chapter 4.5.1](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).</span></span>

## <a name="connect-toohello-server-using-hello-mysql-workbench-gui-tool"></a><span data-ttu-id="2722c-148">Conectar servidor toohello mediante la herramienta de interfaz gráfica de usuario de MySQL Workbench Hola</span><span class="sxs-lookup"><span data-stu-id="2722c-148">Connect toohello server using hello MySQL Workbench GUI tool</span></span>
1.  <span data-ttu-id="2722c-149">Inicie Hola aplicación MySQL Workbench en el equipo cliente.</span><span class="sxs-lookup"><span data-stu-id="2722c-149">Launch hello MySQL Workbench application on your client computer.</span></span> <span data-ttu-id="2722c-150">Puede descargar e instalar MySQL Workbench desde [aquí](https://dev.mysql.com/downloads/workbench/).</span><span class="sxs-lookup"><span data-stu-id="2722c-150">You can download and install MySQL Workbench from [here](https://dev.mysql.com/downloads/workbench/).</span></span>

2.  <span data-ttu-id="2722c-151">Hola **el programa de instalación nueva conexión** diálogo cuadro, escriba Hola siguiente información **parámetros** ficha:</span><span class="sxs-lookup"><span data-stu-id="2722c-151">In hello **Setup New Connection** dialog box, enter hello following information on **Parameters** tab:</span></span>

   ![Configuración de una conexión nueva](./media/quickstart-create-mysql-server-database-using-azure-cli/setup-new-connection.png)

| <span data-ttu-id="2722c-153">**Configuración**</span><span class="sxs-lookup"><span data-stu-id="2722c-153">**Setting**</span></span> | <span data-ttu-id="2722c-154">**Valor sugerido**</span><span class="sxs-lookup"><span data-stu-id="2722c-154">**Suggested Value**</span></span> | <span data-ttu-id="2722c-155">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="2722c-155">**Description**</span></span> |
|---|---|---|
|   <span data-ttu-id="2722c-156">Nombre de la conexión</span><span class="sxs-lookup"><span data-stu-id="2722c-156">Connection Name</span></span> | <span data-ttu-id="2722c-157">Mi conexión</span><span class="sxs-lookup"><span data-stu-id="2722c-157">My Connection</span></span> | <span data-ttu-id="2722c-158">Especifique una etiqueta para esta conexión (puede ser cualquier cosa)</span><span class="sxs-lookup"><span data-stu-id="2722c-158">Specify a label for this connection (this can be anything)</span></span> |
| <span data-ttu-id="2722c-159">Método de conexión</span><span class="sxs-lookup"><span data-stu-id="2722c-159">Connection Method</span></span> | <span data-ttu-id="2722c-160">elija Estándar (TCP/IP)</span><span class="sxs-lookup"><span data-stu-id="2722c-160">choose Standard (TCP/IP)</span></span> | <span data-ttu-id="2722c-161">Usar TCP/IP protocolo tooconnect tooAzure base de datos de MySQL ></span><span class="sxs-lookup"><span data-stu-id="2722c-161">Use TCP/IP protocol tooconnect tooAzure Database for MySQL></span></span> |
| <span data-ttu-id="2722c-162">Nombre de host.</span><span class="sxs-lookup"><span data-stu-id="2722c-162">Hostname</span></span> | <span data-ttu-id="2722c-163">myserver4demo.mysql.database.azure.com</span><span class="sxs-lookup"><span data-stu-id="2722c-163">myserver4demo.mysql.database.azure.com</span></span> | <span data-ttu-id="2722c-164">Nombre del servidor que anotó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2722c-164">Server name you previously noted.</span></span> |
| <span data-ttu-id="2722c-165">Port</span><span class="sxs-lookup"><span data-stu-id="2722c-165">Port</span></span> | <span data-ttu-id="2722c-166">3306</span><span class="sxs-lookup"><span data-stu-id="2722c-166">3306</span></span> | <span data-ttu-id="2722c-167">se utiliza el puerto predeterminado de Hola para MySQL.</span><span class="sxs-lookup"><span data-stu-id="2722c-167">hello default port for MySQL is used.</span></span> |
| <span data-ttu-id="2722c-168">Nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="2722c-168">Username</span></span> | myadmin@myserver4demo | <span data-ttu-id="2722c-169">Hola servidor administrador inicio de sesión que anotó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2722c-169">hello server admin login you previously noted.</span></span> |
| <span data-ttu-id="2722c-170">Password</span><span class="sxs-lookup"><span data-stu-id="2722c-170">Password</span></span> | **** | <span data-ttu-id="2722c-171">Utilice la contraseña de la cuenta de administrador Hola que configuró anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2722c-171">Use hello admin account password you configured earlier.</span></span> |

<span data-ttu-id="2722c-172">Haga clic en **Probar conexión** tootest si todos los parámetros están configurados correctamente.</span><span class="sxs-lookup"><span data-stu-id="2722c-172">Click **Test Connection** tootest if all parameters are correctly configured.</span></span>
<span data-ttu-id="2722c-173">Ahora, puede hacer clic en conexión de hello toosuccessfully conectar toohello server.</span><span class="sxs-lookup"><span data-stu-id="2722c-173">Now, you can click hello connection toosuccessfully connect toohello server.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="2722c-174">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="2722c-174">Clean up resources</span></span>
<span data-ttu-id="2722c-175">Si no necesita estos recursos para otro/tutorial de inicio rápido, puede eliminarlas haciendo Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="2722c-175">If you don't need these resources for another quickstart/tutorial, you can delete them by doing hello following command:</span></span> 

```azurecli-interactive
az group delete --name myresourcegroup
```

## <a name="next-steps"></a><span data-ttu-id="2722c-176">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2722c-176">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2722c-177">Diseño de una base de datos MySQL con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="2722c-177">Design a MySQL Database with Azure CLI</span></span>](./tutorial-design-database-using-cli.md)
