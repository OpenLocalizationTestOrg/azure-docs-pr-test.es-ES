---
title: aaaCreate y administrar la base de datos de Azure con las reglas de firewall de MySQL con CLI de Azure | Documentos de Microsoft
description: "Este artículo se describe cómo toocreate y administrar la base de datos de Azure con las reglas de firewall de MySQL mediante la línea de comandos de CLI de Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: b2f0b4ccf34ce88e3a5e72a64d3f8c78a5bc2a54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-azure-cli"></a><span data-ttu-id="94aa7-103">Creación y administración de reglas de firewall de Azure Database for MySQL mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="94aa7-103">Create and manage Azure Database for MySQL firewall rules using Azure CLI</span></span>
<span data-ttu-id="94aa7-104">Las reglas de firewall de nivel de servidor habilitar administradores toomanage acceso tooan base de datos de MySQL Server desde una dirección IP específica o intervalo de direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="94aa7-104">Server-level firewall rules enable administrators toomanage access tooan Azure Database for MySQL Server from a specific IP address or range of IP addresses.</span></span> <span data-ttu-id="94aa7-105">Usar comandos de CLI de Azure adecuadas, puede crear, actualizar, eliminar, enumerar y mostrar toomanage de reglas de firewall en el servidor.</span><span class="sxs-lookup"><span data-stu-id="94aa7-105">Using convenient Azure CLI commands, you can create, update, delete, list, and show firewall rules toomanage your server.</span></span> <span data-ttu-id="94aa7-106">Para obtener información general sobre los firewalls de Azure Database for MySQL, consulte [Reglas de firewall de un servidor de Azure Database for MySQL](./concepts-firewall-rules.md).</span><span class="sxs-lookup"><span data-stu-id="94aa7-106">For an overview of Azure Database for MySQL firewalls, see [Azure Database for MySQL server firewall rules](./concepts-firewall-rules.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="94aa7-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="94aa7-107">Prerequisites</span></span>
* [<span data-ttu-id="94aa7-108">Instalación de la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="94aa7-108">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-azure-cli)
* <span data-ttu-id="94aa7-109">Instalación del SDK de Python para Azure para los servicios PostgreSQL y MySQL</span><span class="sxs-lookup"><span data-stu-id="94aa7-109">Install Azure Python SDK for PostgreSQL and MySQL Services</span></span>
* <span data-ttu-id="94aa7-110">Instalar el componente de CLI de Azure de Hola para servicios PostgreSQL y MySQL</span><span class="sxs-lookup"><span data-stu-id="94aa7-110">Install hello Azure CLI component for PostgreSQL and MySQL services</span></span>
* <span data-ttu-id="94aa7-111">Creación de un servidor de Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="94aa7-111">Create an Azure Database for MySQL server</span></span>

## <a name="firewall-rule-commands"></a><span data-ttu-id="94aa7-112">Comandos de reglas de firewall:</span><span class="sxs-lookup"><span data-stu-id="94aa7-112">Firewall-Rule Commands:</span></span>
<span data-ttu-id="94aa7-113">Hola **az mysql server regla de firewall** se usa el comando de CLI de Azure toocreate, eliminar, enumerar, mostrar y actualizar las reglas de firewall.</span><span class="sxs-lookup"><span data-stu-id="94aa7-113">hello **az mysql server firewall-rule** command is used from Azure CLI toocreate, delete, list, show, and update firewall rules.</span></span>

<span data-ttu-id="94aa7-114">Comandos:</span><span class="sxs-lookup"><span data-stu-id="94aa7-114">Commands:</span></span>
- <span data-ttu-id="94aa7-115">**create**: crear una regla de firewall de servidor de Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="94aa7-115">**create**: Create an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="94aa7-116">**delete**: eliminar una regla de firewall de servidor de Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="94aa7-116">**delete**: Delete an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="94aa7-117">**lista** : lista de reglas de firewall de servidor hello MySQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="94aa7-117">**list** : List hello Azure MySQL server firewall rules.</span></span>
- <span data-ttu-id="94aa7-118">**Mostrar** : mostrar detalles de Hola de un servidor de MySQL de Azure de regla de firewall.</span><span class="sxs-lookup"><span data-stu-id="94aa7-118">**show** : Show hello details of an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="94aa7-119">**update**: actualizar una regla de firewall de servidor de Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="94aa7-119">**update**: Update an Azure MySQL server firewall rule.</span></span>

## <a name="login-tooazure-and-list-your-azure-database-for-mysql-servers"></a><span data-ttu-id="94aa7-120">TooAzure de inicio de sesión y la lista de la base de datos de Azure para los servidores de MySQL</span><span class="sxs-lookup"><span data-stu-id="94aa7-120">Login tooAzure and List your Azure Database for MySQL Servers</span></span>
<span data-ttu-id="94aa7-121">Conecte de forma segura con la CLI de Azure con su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="94aa7-121">Securely connect Azure CLI with your Azure account.</span></span> <span data-ttu-id="94aa7-122">Hola de uso **inicio de sesión de az** comando toodo esto.</span><span class="sxs-lookup"><span data-stu-id="94aa7-122">Use hello **az login** command toodo this.</span></span>

1. <span data-ttu-id="94aa7-123">Ejecute hello siguiente comando desde la línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="94aa7-123">Run hello following command from hello command line.</span></span>
```azurecli
az login
```
<span data-ttu-id="94aa7-124">Este comando dará como resultado un toouse de código en el paso siguiente de saludo.</span><span class="sxs-lookup"><span data-stu-id="94aa7-124">This command will output a code toouse in hello next step.</span></span>

2. <span data-ttu-id="94aa7-125">Utilizar una página de hello web explorador tooopen [https://aka.ms/devicelogin](https://aka.ms/devicelogin) y escriba el código de hello.</span><span class="sxs-lookup"><span data-stu-id="94aa7-125">Use a web browser tooopen hello page [https://aka.ms/devicelogin](https://aka.ms/devicelogin) and enter hello code.</span></span>

3. <span data-ttu-id="94aa7-126">En el símbolo del sistema de hello, inicie sesión con sus credenciales de Azure.</span><span class="sxs-lookup"><span data-stu-id="94aa7-126">At hello prompt, log in using your Azure credentials.</span></span>

4. <span data-ttu-id="94aa7-127">Una vez que se autoriza su inicio de sesión, se imprimirá una lista de suscripciones en la consola de Hola.</span><span class="sxs-lookup"><span data-stu-id="94aa7-127">Once your login is authorized, a list of subscriptions will be printed in hello console.</span></span> <span data-ttu-id="94aa7-128">Copie el identificador de Hola de hello deseado suscripción tooset Hola actual suscripción toobe utilizado en el futuro.</span><span class="sxs-lookup"><span data-stu-id="94aa7-128">Copy hello id of hello desired subscription tooset hello current subscription toobe used moving forward.</span></span>
   ```azurecli-interactive
   az account set --subscription {your subscription id}
   ```

5. <span data-ttu-id="94aa7-129">Si no está seguro de los nombres de Hola se enumeran hello las bases de datos de Azure para servidores de MySQL Server para el grupo de recursos y de suscripción.</span><span class="sxs-lookup"><span data-stu-id="94aa7-129">List hello Azure Databases for MySQL servers for your subscription and resource group if you are unsure of hello names.</span></span>

   ```azurecli-interactive
   az mysql server list --resource-group myResourceGroup
   ```

   <span data-ttu-id="94aa7-130">Tenga en cuenta atributo de nombre de Hola Hola enumerar, que será usado toospecify qué toowork de servidor MySQL en.</span><span class="sxs-lookup"><span data-stu-id="94aa7-130">Note hello name attribute in hello listing, which will be used toospecify which MySQL server toowork on.</span></span> <span data-ttu-id="94aa7-131">Si es necesario, confirme los detalles de Hola para ese nombre tooconfirm del atributo de nombre de servidor toousing hello es correcta:</span><span class="sxs-lookup"><span data-stu-id="94aa7-131">If needed, confirm hello details for that server toousing hello name attribute tooconfirm name is correct:</span></span>

   ```azurecli-interactive
   az mysql server show --resource-group myResourceGroup --name mysqlserver4demo
   ```

## <a name="list-firewall-rules-on-azure-database-for-mysql-server"></a><span data-ttu-id="94aa7-132">Lista de reglas de firewall en el servidor de Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="94aa7-132">List Firewall Rules on Azure Database for MySQL Server</span></span> 
<span data-ttu-id="94aa7-133">Utilizando el nombre del servidor de Hola y nombre de grupo de recursos de hello, reglas de firewall servidor existente de lista de hello en el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="94aa7-133">Using hello server name and hello resource group name, list hello existing server firewall rules on hello server.</span></span> <span data-ttu-id="94aa7-134">Observe cómo se especifica dicho atributo de nombre de servidor de Hola Hola **--servidor** cambia y no Hola **--nombre** cambiar.</span><span class="sxs-lookup"><span data-stu-id="94aa7-134">Notice that hello server name attribute is specified in hello **--server** switch and not hello **--name** switch.</span></span>
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo
```
<span data-ttu-id="94aa7-135">salida de Hello mostrará las reglas de hello si los hay, de forma predeterminada en JSON de formato.</span><span class="sxs-lookup"><span data-stu-id="94aa7-135">hello output will list hello rules if any, by default in JSON format.</span></span> <span data-ttu-id="94aa7-136">Puede usar el modificador de hello **: tabla de salida** para un formato más legible de la tabla como resultado de hello.</span><span class="sxs-lookup"><span data-stu-id="94aa7-136">You may use hello switch **--output table** for a more readable table format as hello output.</span></span>
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo --output table
```
## <a name="create-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="94aa7-137">Creación de reglas de firewall en el servidor de Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="94aa7-137">Create Firewall Rule on Azure Database for MySQL Server</span></span>
<span data-ttu-id="94aa7-138">Con nombre del servidor de MySQL de Azure de Hola y el nombre de grupo de recursos de hello, cree una nueva regla de firewall en el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="94aa7-138">Using hello Azure MySQL server name and hello resource group name, create a new firewall rule on hello server.</span></span> <span data-ttu-id="94aa7-139">Proporcione un nombre para la regla de Hola y Hola inicio IP, IP final para hello regla toocover un intervalo de direcciones IP tooallow acceda.</span><span class="sxs-lookup"><span data-stu-id="94aa7-139">Provide a name for hello rule, hello start IP, and end IP for hello rule toocover a range of IP addresses tooallow access.</span></span>
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.15
```
<span data-ttu-id="94aa7-140">Para una dirección IP singular direcciones toobe puede tener acceso, proporcione Hola la misma dirección como Hola IP inicial y final de IP, como en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="94aa7-140">For a singular IP address toobe allowed access, provide hello same address as hello Start IP and End IP, as in this example.</span></span>
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  
--server mysql --name "Firewall Rule with a Single Address" --start-ip-address 1.1.1.1 --end-ip-address 1.1.1.1
```
<span data-ttu-id="94aa7-141">Cuando se realiza correctamente, el resultado del comando de hello mostrará detalles Hola Hola de regla de firewall que ha creado, de forma predeterminada en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="94aa7-141">Upon success, hello command output will list hello details of hello firewall rule you have created, by default in JSON format.</span></span> <span data-ttu-id="94aa7-142">Si se produce un error, el resultado de hello mostrará el texto del mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="94aa7-142">If there is a failure, hello output will show error message text instead.</span></span>

## <a name="update-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="94aa7-143">Actualización de reglas de firewall en el servidor de Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="94aa7-143">Update Firewall Rule on Azure Database for MySQL server</span></span> 
<span data-ttu-id="94aa7-144">Con nombre del servidor de MySQL de Azure de Hola y el nombre de grupo de recursos de hello, actualizar una regla de firewall existente en el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="94aa7-144">Using hello Azure MySQL server name and hello resource group name, update an existing firewall rule on hello server.</span></span> <span data-ttu-id="94aa7-145">Proporcione el nombre de Hola de regla de firewall existente hello como entrada y Hola inicio IP y final IP atributos tooupdate.</span><span class="sxs-lookup"><span data-stu-id="94aa7-145">Provide hello name of hello existing firewall rule as input, and hello start IP and end IP attributes tooupdate.</span></span>
```azurecli-interactive
az mysql server firewall-rule update --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.1
```
<span data-ttu-id="94aa7-146">Cuando se realiza correctamente, el resultado del comando de hello mostrará detalles Hola Hola de regla de firewall que ha actualizado, de forma predeterminada en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="94aa7-146">Upon success, hello command output will list hello details of hello firewall rule you have updated, by default in JSON format.</span></span> <span data-ttu-id="94aa7-147">Si se produce un error, el resultado de hello mostrará el texto del mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="94aa7-147">If there is a failure, hello output will show error message text instead.</span></span>

> [!NOTE]
> <span data-ttu-id="94aa7-148">Si la regla de firewall de hello no existe, se creará mediante el comando de actualización de Hola.</span><span class="sxs-lookup"><span data-stu-id="94aa7-148">If hello firewall rule does not exist, it will be created by hello update command.</span></span>

## <a name="show-firewall-rule-details-on-azure-database-for-mysql-server"></a><span data-ttu-id="94aa7-149">Presentación de los detalles de las reglas de firewall en el servidor de Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="94aa7-149">Show Firewall Rule Details on Azure Database for MySQL Server</span></span>
<span data-ttu-id="94aa7-150">Con el nombre del servidor de MySQL de Azure de Hola y el nombre de grupo de recursos de hello, mostrar detalles de regla de firewall existente de Hola desde servidor hello.</span><span class="sxs-lookup"><span data-stu-id="94aa7-150">Using hello Azure MySQL server name and hello resource group name, show hello existing firewall rule details from hello server.</span></span> <span data-ttu-id="94aa7-151">Proporcione el nombre de Hola de regla de firewall existente hello como entrada.</span><span class="sxs-lookup"><span data-stu-id="94aa7-151">Provide hello name of hello existing firewall rule as input.</span></span>
```azurecli-interactive
az mysql server firewall-rule show --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
<span data-ttu-id="94aa7-152">Cuando se realiza correctamente, el resultado del comando de hello mostrará detalles Hola Hola de regla de firewall que ha especificado, de forma predeterminada en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="94aa7-152">Upon success, hello command output will list hello details of hello firewall rule you have specified, by default in JSON format.</span></span> <span data-ttu-id="94aa7-153">Si se produce un error, el resultado de hello mostrará el texto del mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="94aa7-153">If there is a failure, hello output will show error message text instead.</span></span>

## <a name="delete-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="94aa7-154">Eliminación de reglas de firewall en el servidor de Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="94aa7-154">Delete Firewall Rule on Azure Database for MySQL Server</span></span>
<span data-ttu-id="94aa7-155">Con el nombre del servidor de MySQL de Azure de Hola y el nombre de grupo de recursos de hello, quite una regla de firewall existente del servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="94aa7-155">Using hello Azure MySQL server name and hello resource group name, remove an existing firewall rule from hello server.</span></span> <span data-ttu-id="94aa7-156">Proporcione el nombre de Hola Hola existente de regla de firewall.</span><span class="sxs-lookup"><span data-stu-id="94aa7-156">Provide hello name of hello existing firewall rule.</span></span>
```azurecli-interactive
az mysql server firewall-rule delete --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
<span data-ttu-id="94aa7-157">Cuando se realiza correctamente, no hay ninguna salida.</span><span class="sxs-lookup"><span data-stu-id="94aa7-157">Upon success, there is no output.</span></span> <span data-ttu-id="94aa7-158">En caso de error, se devolverá el texto del mensaje de error de Hola.</span><span class="sxs-lookup"><span data-stu-id="94aa7-158">Upon failure, hello error message text will be returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="94aa7-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="94aa7-159">Next steps</span></span>
- <span data-ttu-id="94aa7-160">Para más información, consulte [Reglas de firewall de servidor de Azure Database for MySQL](./concepts-firewall-rules.md).</span><span class="sxs-lookup"><span data-stu-id="94aa7-160">Understand more about [Azure Database for MySQL Server firewall rules](./concepts-firewall-rules.md)</span></span>
- [<span data-ttu-id="94aa7-161">Crear y administrar la base de datos de Azure para las reglas de firewall de MySQL con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="94aa7-161">Create and manage Azure Database for MySQL firewall rules using hello Azure portal</span></span>](./howto-manage-firewall-using-portal.md)
