---
title: "Creación y administración de reglas de firewall de Azure Database for MySQL mediante la CLI de Azure | Microsoft Docs"
description: "Este artículo describe cómo crear y administrar reglas de firewall de Azure Database for MySQL mediante la línea de comandos de la CLI de Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 9a03722e9f71be307bdbf0b846a4cbf7b34cd7ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-azure-cli"></a><span data-ttu-id="efe59-103">Creación y administración de reglas de firewall de Azure Database for MySQL mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="efe59-103">Create and manage Azure Database for MySQL firewall rules using Azure CLI</span></span>
<span data-ttu-id="efe59-104">Las reglas de firewall de nivel de servidor permiten a los administradores administrar el acceso a un servidor de Azure Database for MySQL desde una dirección IP o desde un intervalo de direcciones IP especificado.</span><span class="sxs-lookup"><span data-stu-id="efe59-104">Server-level firewall rules enable administrators to manage access to an Azure Database for MySQL Server from a specific IP address or range of IP addresses.</span></span> <span data-ttu-id="efe59-105">Con los comandos de la CLI de Azure adecuados, puede crear, actualizar, eliminar, enumerar y mostrar reglas de firewall para administrar el servidor.</span><span class="sxs-lookup"><span data-stu-id="efe59-105">Using convenient Azure CLI commands, you can create, update, delete, list, and show firewall rules to manage your server.</span></span> <span data-ttu-id="efe59-106">Para obtener información general sobre los firewalls de Azure Database for MySQL, consulte [Reglas de firewall de un servidor de Azure Database for MySQL](./concepts-firewall-rules.md).</span><span class="sxs-lookup"><span data-stu-id="efe59-106">For an overview of Azure Database for MySQL firewalls, see [Azure Database for MySQL server firewall rules](./concepts-firewall-rules.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="efe59-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="efe59-107">Prerequisites</span></span>
* [<span data-ttu-id="efe59-108">Instalación de la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="efe59-108">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-azure-cli)
* <span data-ttu-id="efe59-109">Instalación del SDK de Python para Azure para los servicios PostgreSQL y MySQL</span><span class="sxs-lookup"><span data-stu-id="efe59-109">Install Azure Python SDK for PostgreSQL and MySQL Services</span></span>
* <span data-ttu-id="efe59-110">Instalación del componente de la CLI de Azure para los servicios PostgreSQL y MySQL</span><span class="sxs-lookup"><span data-stu-id="efe59-110">Install the Azure CLI component for PostgreSQL and MySQL services</span></span>
* <span data-ttu-id="efe59-111">Creación de un servidor de Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="efe59-111">Create an Azure Database for MySQL server</span></span>

## <a name="firewall-rule-commands"></a><span data-ttu-id="efe59-112">Comandos de reglas de firewall:</span><span class="sxs-lookup"><span data-stu-id="efe59-112">Firewall-Rule Commands:</span></span>
<span data-ttu-id="efe59-113">El comando **az mysql server firewall-rule** se utiliza desde la CLI de Azure para crear, eliminar, enumerar, mostrar y actualizar reglas de firewall.</span><span class="sxs-lookup"><span data-stu-id="efe59-113">The **az mysql server firewall-rule** command is used from Azure CLI to create, delete, list, show, and update firewall rules.</span></span>

<span data-ttu-id="efe59-114">Comandos:</span><span class="sxs-lookup"><span data-stu-id="efe59-114">Commands:</span></span>
- <span data-ttu-id="efe59-115">**create**: crear una regla de firewall de servidor de Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="efe59-115">**create**: Create an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="efe59-116">**delete**: eliminar una regla de firewall de servidor de Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="efe59-116">**delete**: Delete an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="efe59-117">**list**: enumerar las reglas de firewall de servidor de Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="efe59-117">**list** : List the Azure MySQL server firewall rules.</span></span>
- <span data-ttu-id="efe59-118">**show**: mostrar los detalles de una regla de firewall de servidor de Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="efe59-118">**show** : Show the details of an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="efe59-119">**update**: actualizar una regla de firewall de servidor de Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="efe59-119">**update**: Update an Azure MySQL server firewall rule.</span></span>

## <a name="login-to-azure-and-list-your-azure-database-for-mysql-servers"></a><span data-ttu-id="efe59-120">Inicio de sesión en Azure y lista de los servidores de Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="efe59-120">Login to Azure and List your Azure Database for MySQL Servers</span></span>
<span data-ttu-id="efe59-121">Conecte de forma segura con la CLI de Azure con su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="efe59-121">Securely connect Azure CLI with your Azure account.</span></span> <span data-ttu-id="efe59-122">Use el comando **az login** para hacerlo.</span><span class="sxs-lookup"><span data-stu-id="efe59-122">Use the **az login** command to do this.</span></span>

1. <span data-ttu-id="efe59-123">Ejecute el siguiente comando desde la línea de comando.</span><span class="sxs-lookup"><span data-stu-id="efe59-123">Run the following command from the command line.</span></span>
```azurecli
az login
```
<span data-ttu-id="efe59-124">Este comando generará un código que se usará en el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="efe59-124">This command will output a code to use in the next step.</span></span>

2. <span data-ttu-id="efe59-125">Use un explorador web para abrir la página [https://aka.ms/devicelogin](https://aka.ms/devicelogin) y escriba el código.</span><span class="sxs-lookup"><span data-stu-id="efe59-125">Use a web browser to open the page [https://aka.ms/devicelogin](https://aka.ms/devicelogin) and enter the code.</span></span>

3. <span data-ttu-id="efe59-126">En el mensaje, inicie sesión con sus credenciales de Azure.</span><span class="sxs-lookup"><span data-stu-id="efe59-126">At the prompt, log in using your Azure credentials.</span></span>

4. <span data-ttu-id="efe59-127">Una vez que se autoriza su inicio de sesión, se imprimirá una lista de suscripciones en la consola.</span><span class="sxs-lookup"><span data-stu-id="efe59-127">Once your login is authorized, a list of subscriptions will be printed in the console.</span></span> <span data-ttu-id="efe59-128">Copie el identificador de la suscripción deseada para establecer que la suscripción actual se usará a partir de ahora.</span><span class="sxs-lookup"><span data-stu-id="efe59-128">Copy the id of the desired subscription to set the current subscription to be used moving forward.</span></span>
   ```azurecli-interactive
   az account set --subscription {your subscription id}
   ```

5. <span data-ttu-id="efe59-129">Si no está seguro de los nombres, muestre los servidores de Azure Database for MySQL para su suscripción y grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="efe59-129">List the Azure Databases for MySQL servers for your subscription and resource group if you are unsure of the names.</span></span>

   ```azurecli-interactive
   az mysql server list --resource-group myResourceGroup
   ```

   <span data-ttu-id="efe59-130">Anote el valor del atributo name de la lista, que se usará para especificar con qué servidor MySQL desea trabajar.</span><span class="sxs-lookup"><span data-stu-id="efe59-130">Note the name attribute in the listing, which will be used to specify which MySQL server to work on.</span></span> <span data-ttu-id="efe59-131">Si es necesario, confirme los detalles de dicho servidor con el atributo name para confirmar que el nombre es correcto:</span><span class="sxs-lookup"><span data-stu-id="efe59-131">If needed, confirm the details for that server to using the name attribute to confirm name is correct:</span></span>

   ```azurecli-interactive
   az mysql server show --resource-group myResourceGroup --name mysqlserver4demo
   ```

## <a name="list-firewall-rules-on-azure-database-for-mysql-server"></a><span data-ttu-id="efe59-132">Lista de reglas de firewall en el servidor de Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="efe59-132">List Firewall Rules on Azure Database for MySQL Server</span></span> 
<span data-ttu-id="efe59-133">Utilizando el nombre del servidor y el nombre del grupo de recursos, enumere las reglas de firewall existentes en el servidor.</span><span class="sxs-lookup"><span data-stu-id="efe59-133">Using the server name and the resource group name, list the existing server firewall rules on the server.</span></span> <span data-ttu-id="efe59-134">Tenga en cuenta que el atributo de nombre de servidor se especifica en el modificador **--server** y no en el modificador **--name**.</span><span class="sxs-lookup"><span data-stu-id="efe59-134">Notice that the server name attribute is specified in the **--server** switch and not the **--name** switch.</span></span>
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo
```
<span data-ttu-id="efe59-135">La salida mostrará las reglas existentes, de forma predeterminada en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="efe59-135">The output will list the rules if any, by default in JSON format.</span></span> <span data-ttu-id="efe59-136">Puede usar la opción **--output table** para obtener una salida en formato de tabla más legible.</span><span class="sxs-lookup"><span data-stu-id="efe59-136">You may use the switch **--output table** for a more readable table format as the output.</span></span>
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo --output table
```
## <a name="create-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="efe59-137">Creación de reglas de firewall en el servidor de Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="efe59-137">Create Firewall Rule on Azure Database for MySQL Server</span></span>
<span data-ttu-id="efe59-138">Con el nombre del servidor de Azure MySQL y el nombre del grupo de recursos, cree una nueva regla de firewall en el servidor.</span><span class="sxs-lookup"><span data-stu-id="efe59-138">Using the Azure MySQL server name and the resource group name, create a new firewall rule on the server.</span></span> <span data-ttu-id="efe59-139">Dé un nombre a la regla y las direcciones IP inicial y final para designar un intervalo de direcciones IP al que se permitirá el acceso.</span><span class="sxs-lookup"><span data-stu-id="efe59-139">Provide a name for the rule, the start IP, and end IP for the rule to cover a range of IP addresses to allow access.</span></span>
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.15
```
<span data-ttu-id="efe59-140">Para permitir el acceso a una única dirección IP, proporcione la misma dirección como dirección IP de inicio y de final, como en el ejemplo.</span><span class="sxs-lookup"><span data-stu-id="efe59-140">For a singular IP address to be allowed access, provide the same address as the Start IP and End IP, as in this example.</span></span>
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  
--server mysql --name "Firewall Rule with a Single Address" --start-ip-address 1.1.1.1 --end-ip-address 1.1.1.1
```
<span data-ttu-id="efe59-141">Cuando se realiza correctamente, la salida del comando mostrará los detalles de la regla de firewall que ha creado, de forma predeterminada en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="efe59-141">Upon success, the command output will list the details of the firewall rule you have created, by default in JSON format.</span></span> <span data-ttu-id="efe59-142">Si se produce un error, la salida mostrará el texto del mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="efe59-142">If there is a failure, the output will show error message text instead.</span></span>

## <a name="update-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="efe59-143">Actualización de reglas de firewall en el servidor de Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="efe59-143">Update Firewall Rule on Azure Database for MySQL server</span></span> 
<span data-ttu-id="efe59-144">Con el nombre del servidor de Azure MySQL y el nombre del grupo de recursos, actualice una regla de firewall existente en el servidor.</span><span class="sxs-lookup"><span data-stu-id="efe59-144">Using the Azure MySQL server name and the resource group name, update an existing firewall rule on the server.</span></span> <span data-ttu-id="efe59-145">Proporcione como entrada el nombre de una regla de firewall existente y los atributos de dirección IP de inicio y final que se van a actualizar.</span><span class="sxs-lookup"><span data-stu-id="efe59-145">Provide the name of the existing firewall rule as input, and the start IP and end IP attributes to update.</span></span>
```azurecli-interactive
az mysql server firewall-rule update --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.1
```
<span data-ttu-id="efe59-146">Cuando se realiza correctamente, la salida del comando mostrará los detalles de la regla de firewall que ha actualizado, de forma predeterminada en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="efe59-146">Upon success, the command output will list the details of the firewall rule you have updated, by default in JSON format.</span></span> <span data-ttu-id="efe59-147">Si se produce un error, la salida mostrará el texto del mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="efe59-147">If there is a failure, the output will show error message text instead.</span></span>

> [!NOTE]
> <span data-ttu-id="efe59-148">Si la regla de firewall no existe, el comando update la creará.</span><span class="sxs-lookup"><span data-stu-id="efe59-148">If the firewall rule does not exist, it will be created by the update command.</span></span>

## <a name="show-firewall-rule-details-on-azure-database-for-mysql-server"></a><span data-ttu-id="efe59-149">Presentación de los detalles de las reglas de firewall en el servidor de Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="efe59-149">Show Firewall Rule Details on Azure Database for MySQL Server</span></span>
<span data-ttu-id="efe59-150">Con el nombre del servidor de Azure MySQL y el nombre del grupo de recursos, muestre los detalles de la regla de firewall existente en el servidor.</span><span class="sxs-lookup"><span data-stu-id="efe59-150">Using the Azure MySQL server name and the resource group name, show the existing firewall rule details from the server.</span></span> <span data-ttu-id="efe59-151">Proporcione como entrada el nombre de una regla de firewall existente.</span><span class="sxs-lookup"><span data-stu-id="efe59-151">Provide the name of the existing firewall rule as input.</span></span>
```azurecli-interactive
az mysql server firewall-rule show --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
<span data-ttu-id="efe59-152">Cuando se realiza correctamente, la salida del comando mostrará los detalles de la regla de firewall que ha especificado, de forma predeterminada en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="efe59-152">Upon success, the command output will list the details of the firewall rule you have specified, by default in JSON format.</span></span> <span data-ttu-id="efe59-153">Si se produce un error, la salida mostrará el texto del mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="efe59-153">If there is a failure, the output will show error message text instead.</span></span>

## <a name="delete-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="efe59-154">Eliminación de reglas de firewall en el servidor de Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="efe59-154">Delete Firewall Rule on Azure Database for MySQL Server</span></span>
<span data-ttu-id="efe59-155">Con el nombre del servidor de Azure MySQL y el nombre del grupo de recursos, quite una regla de firewall existente del servidor.</span><span class="sxs-lookup"><span data-stu-id="efe59-155">Using the Azure MySQL server name and the resource group name, remove an existing firewall rule from the server.</span></span> <span data-ttu-id="efe59-156">Proporcione el nombre de una regla de firewall existente.</span><span class="sxs-lookup"><span data-stu-id="efe59-156">Provide the name of the existing firewall rule.</span></span>
```azurecli-interactive
az mysql server firewall-rule delete --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
<span data-ttu-id="efe59-157">Cuando se realiza correctamente, no hay ninguna salida.</span><span class="sxs-lookup"><span data-stu-id="efe59-157">Upon success, there is no output.</span></span> <span data-ttu-id="efe59-158">En caso de error, se devolverá el texto del mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="efe59-158">Upon failure, the error message text will be returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="efe59-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="efe59-159">Next steps</span></span>
- <span data-ttu-id="efe59-160">Para más información, consulte [Reglas de firewall de servidor de Azure Database for MySQL](./concepts-firewall-rules.md).</span><span class="sxs-lookup"><span data-stu-id="efe59-160">Understand more about [Azure Database for MySQL Server firewall rules](./concepts-firewall-rules.md)</span></span>
- [<span data-ttu-id="efe59-161">Creación y administración de reglas de firewall de Azure Database for MySQL mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="efe59-161">Create and manage Azure Database for MySQL firewall rules using the Azure portal</span></span>](./howto-manage-firewall-using-portal.md)
