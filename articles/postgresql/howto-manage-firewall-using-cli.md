---
title: "Creación y administración de reglas de firewall de Azure Database for PostgreSQL mediante la CLI de Azure | Microsoft Docs"
description: "En este artículo se describe cómo crear y administrar reglas de firewall de Azure Database for PostgreSQL mediante la línea de comandos de Azure."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 6f081416dd7d78f0153b3fda21a340a8c1a70c5f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-azure-cli"></a><span data-ttu-id="df13d-103">Creación y administración de reglas de firewall de Azure Database for PostgreSQL mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="df13d-103">Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI</span></span>
<span data-ttu-id="df13d-104">Las reglas de firewall de nivel de servidor permiten a los administradores administrar el acceso a un servidor de Azure Database for PostgreSQL desde una dirección IP o desde un intervalo de direcciones IP especificado.</span><span class="sxs-lookup"><span data-stu-id="df13d-104">Server-level firewall rules enable administrators to manage access to an Azure Database for PostgreSQL Server from a specific IP address or range of IP addresses.</span></span> <span data-ttu-id="df13d-105">Con los comandos de la CLI de Azure adecuados, puede crear, actualizar, eliminar, enumerar y mostrar reglas de firewall para administrar el servidor.</span><span class="sxs-lookup"><span data-stu-id="df13d-105">Using convenient Azure CLI commands, you can create, update, delete, list, and show firewall rules to manage your server.</span></span> <span data-ttu-id="df13d-106">Para obtener información general sobre los firewalls de Azure Database for PostgreSQL, consulte [Reglas de firewall de un servidor de Azure Database for PostgreSQL](concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="df13d-106">For an overview of Azure Database for PostgreSQL firewalls, see [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="df13d-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="df13d-107">Prerequisites</span></span>
<span data-ttu-id="df13d-108">Para seguir esta guía, necesitará:</span><span class="sxs-lookup"><span data-stu-id="df13d-108">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="df13d-109">Un [servidor y una base de datos de Azure Database for PostgreSQL](quickstart-create-server-database-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="df13d-109">An [Azure Database for PostgreSQL server and database](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="df13d-110">Instalar la utilidad de línea de comandos [Azure CLI 2.0](/cli/azure/install-azure-cli) o usar Azure Cloud Shell en el explorador.</span><span class="sxs-lookup"><span data-stu-id="df13d-110">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command line utility or use the Azure Cloud Shell in the browser.</span></span>

## <a name="configure-firewall-rules-for-azure-database-for-postgresql"></a><span data-ttu-id="df13d-111">Configuración de reglas de firewall para Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="df13d-111">Configure firewall rules for Azure Database for PostgreSQL</span></span>
<span data-ttu-id="df13d-112">Los comandos [az postgres server firewall-rule](/cli/azure/postgres/server/firewall-rule) se usan para configurar reglas de firewall.</span><span class="sxs-lookup"><span data-stu-id="df13d-112">The [az postgres server firewall-rule](/cli/azure/postgres/server/firewall-rule) commands are used to configure firewall rules.</span></span>

## <a name="list-firewall-rules"></a><span data-ttu-id="df13d-113">Enumerar reglas de firewall</span><span class="sxs-lookup"><span data-stu-id="df13d-113">List firewall rules</span></span> 
<span data-ttu-id="df13d-114">Para enumerar las reglas de firewall de servidor existentes en el servidor, ejecute el comando [az postgres server firewall-rule list](/cli/azure/postgres/server/firewall-rule#list).</span><span class="sxs-lookup"><span data-stu-id="df13d-114">To list the existing server firewall rules on the server, run the [az postgres server firewall-rule list](/cli/azure/postgres/server/firewall-rule#list) command.</span></span>
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401
```
<span data-ttu-id="df13d-115">La salida enumera las reglas existentes, si existen, en formato JSON de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="df13d-115">The output lists the rules if any, by default in JSON format.</span></span> <span data-ttu-id="df13d-116">Puede usar el modificador `--output table` para obtener una salida en formato de tabla más legible.</span><span class="sxs-lookup"><span data-stu-id="df13d-116">You may use the switch `--output table` for a more readable table format as the output.</span></span>
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401 --output table
```
## <a name="create-firewall-rule"></a><span data-ttu-id="df13d-117">Crear reglas de firewall</span><span class="sxs-lookup"><span data-stu-id="df13d-117">Create firewall rule</span></span>
<span data-ttu-id="df13d-118">Para crear una regla de firewall en el servidor, ejecute el comando [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create).</span><span class="sxs-lookup"><span data-stu-id="df13d-118">To create a new firewall rule on the server, run the [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> 

<span data-ttu-id="df13d-119">En este ejemplo se permite a un rango de todas las direcciones IP tener acceso al servidor **mypgserver-20170401.postgres.database.azure.com**</span><span class="sxs-lookup"><span data-stu-id="df13d-119">This example allows a range of all IP addresses to access the server **mypgserver-20170401.postgres.database.azure.com**</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
<span data-ttu-id="df13d-120">Para permitir el acceso a una única dirección IP, proporcione la misma dirección como dirección IP inicial y final, como en el ejemplo.</span><span class="sxs-lookup"><span data-stu-id="df13d-120">To allow a singular IP address to access, provide the same address as the Start IP and End IP, as in this example.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  
--server mypgserver-20170401 --name "AllowSingleIpAddress" --start-ip-address 13.83.152.1 --end-ip-address 13.83.152.1
```
<span data-ttu-id="df13d-121">Si se realiza correctamente, la salida del comando muestra los detalles de la regla de firewall que ha creado, de forma predeterminada en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="df13d-121">Upon success, the command output lists the details of the firewall rule you have created, by default in JSON format.</span></span> <span data-ttu-id="df13d-122">Si se produce un error, la salida muestra el texto del mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="df13d-122">If there is a failure, the output showserror message text instead.</span></span>

## <a name="update-firewall-rule"></a><span data-ttu-id="df13d-123">Actualizar reglas de firewall</span><span class="sxs-lookup"><span data-stu-id="df13d-123">Update firewall rule</span></span> 
<span data-ttu-id="df13d-124">Se puede actualizar una regla de firewall existente en el servidor con el comando [az postgres server firewall-rule update](/cli/azure/postgres/server/firewall-rule#update).</span><span class="sxs-lookup"><span data-stu-id="df13d-124">Update an existing firewall rule on the server using [az postgres server firewall-rule update](/cli/azure/postgres/server/firewall-rule#update) command.</span></span> <span data-ttu-id="df13d-125">Proporcione como entrada el nombre de una regla de firewall existente y los atributos de dirección IP de inicio y final que se van a actualizar.</span><span class="sxs-lookup"><span data-stu-id="df13d-125">Provide the name of the existing firewall rule as input, and the start IP and end IP attributes to update.</span></span>
```azurecli-interactive
az postgres server firewall-rule update --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.255
```
<span data-ttu-id="df13d-126">Cuando se realiza correctamente, la salida del comando muestra los detalles de la regla de firewall que ha actualizado, de forma predeterminada en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="df13d-126">Upon success, the command output lists the details of the firewall rule you have updated, by default in JSON format.</span></span> <span data-ttu-id="df13d-127">Si se produce un error, la salida muestra el texto del mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="df13d-127">If there is a failure, the output showserror message text instead.</span></span>
> [!NOTE]
> <span data-ttu-id="df13d-128">Si la regla de firewall no existe, el comando update la crea.</span><span class="sxs-lookup"><span data-stu-id="df13d-128">If the firewall rule does not exist, it gets created by the update command.</span></span>

## <a name="show-firewall-rule-details"></a><span data-ttu-id="df13d-129">Mostrar los detalles de la regla de firewall</span><span class="sxs-lookup"><span data-stu-id="df13d-129">Show firewall rule details</span></span>
<span data-ttu-id="df13d-130">También puede mostrar los detalles de la regla de firewall existente para un servidor mediante la ejecución del comando [az postgres server firewall-rule show](/cli/azure/postgres/server/firewall-rule#show).</span><span class="sxs-lookup"><span data-stu-id="df13d-130">You can also show the existing firewall rule details for a server by running [az postgres server firewall-rule show](/cli/azure/postgres/server/firewall-rule#show) command.</span></span>
```azurecli-interactive
az postgres server firewall-rule show --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
<span data-ttu-id="df13d-131">Cuando se realiza correctamente, la salida del comando muestra los detalles de la regla de firewall que ha especificado, de forma predeterminada en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="df13d-131">Upon success, the command output lists the details of the firewall rule you have specified, by default in JSON format.</span></span> <span data-ttu-id="df13d-132">Si se produce un error, la salida muestra el texto del mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="df13d-132">If there is a failure, the output showserror message text instead.</span></span>

## <a name="delete-firewall-rule"></a><span data-ttu-id="df13d-133">Eliminar reglas de firewall</span><span class="sxs-lookup"><span data-stu-id="df13d-133">Delete firewall rule</span></span>
<span data-ttu-id="df13d-134">Para revocar el acceso de un intervalo IP desde el servidor, elimine una regla de firewall existente mediante la ejecución del comando [az postgres server firewall-rule delete](/cli/azure/postgres/server/firewall-rule#delete).</span><span class="sxs-lookup"><span data-stu-id="df13d-134">To revoke access for an IP range from the server, delete an existing firewall rule by executing the [az postgres server firewall-rule delete](/cli/azure/postgres/server/firewall-rule#delete) command.</span></span> <span data-ttu-id="df13d-135">Proporcione el nombre de una regla de firewall existente.</span><span class="sxs-lookup"><span data-stu-id="df13d-135">Provide the name of the existing firewall rule.</span></span>
```azurecli-interactive
az postgres server firewall-rule delete --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
<span data-ttu-id="df13d-136">Cuando se realiza correctamente, no hay ninguna salida.</span><span class="sxs-lookup"><span data-stu-id="df13d-136">Upon success, there is no output.</span></span> <span data-ttu-id="df13d-137">En caso de error, se devuelve el texto del mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="df13d-137">Upon failure, the error message text is returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="df13d-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="df13d-138">Next steps</span></span>
- <span data-ttu-id="df13d-139">De forma similar, puede utilizar un explorador web para [crear y administrar reglas de firewall de Azure Database for PostgreSQL mediante Azure Portal](howto-manage-firewall-using-portal.md).</span><span class="sxs-lookup"><span data-stu-id="df13d-139">Similarly, you can use a web browser to [Create and manage Azure Database for PostgreSQL firewall rules using the Azure portal](howto-manage-firewall-using-portal.md)</span></span>
- <span data-ttu-id="df13d-140">Para más información, consulte [Reglas de firewall de servidor de Azure Database for PostgreSQL](concepts-firewall-rules.md).</span><span class="sxs-lookup"><span data-stu-id="df13d-140">Understand more about [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md)</span></span>
- <span data-ttu-id="df13d-141">Para obtener ayuda para la conexión a un servidor de Azure Database for PostgreSQL, consulte [Bibliotecas de conexión para Azure Database for PostgreSQL](concepts-connection-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="df13d-141">For help in connecting to an Azure Database for PostgreSQL server, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
