---
title: aaaCreate y administrar la base de datos PostgreSQL las reglas de firewall mediante la CLI de Azure | Documentos de Microsoft
description: "Este artículo se describe cómo toocreate y administrar la base de datos PostgreSQL las reglas de firewall mediante la línea de comandos de CLI de Azure."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 06e34c9e3996c2ec3df63191d794bc34d0ca0cf2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-azure-cli"></a><span data-ttu-id="0dbb1-103">Creación y administración de reglas de firewall de Azure Database for PostgreSQL mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="0dbb1-103">Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI</span></span>
<span data-ttu-id="0dbb1-104">Las reglas de firewall de nivel de servidor habilitar administradores toomanage acceso tooan base de datos de Azure para PostgreSQL Server desde una dirección IP específica o intervalo de direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="0dbb1-104">Server-level firewall rules enable administrators toomanage access tooan Azure Database for PostgreSQL Server from a specific IP address or range of IP addresses.</span></span> <span data-ttu-id="0dbb1-105">Usar comandos de CLI de Azure adecuadas, puede crear, actualizar, eliminar, enumerar y mostrar toomanage de reglas de firewall en el servidor.</span><span class="sxs-lookup"><span data-stu-id="0dbb1-105">Using convenient Azure CLI commands, you can create, update, delete, list, and show firewall rules toomanage your server.</span></span> <span data-ttu-id="0dbb1-106">Para obtener información general sobre los firewalls de Azure Database for PostgreSQL, consulte [Reglas de firewall de un servidor de Azure Database for PostgreSQL](concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="0dbb1-106">For an overview of Azure Database for PostgreSQL firewalls, see [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0dbb1-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0dbb1-107">Prerequisites</span></span>
<span data-ttu-id="0dbb1-108">toostep a través de este tooguide cómo, necesita:</span><span class="sxs-lookup"><span data-stu-id="0dbb1-108">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="0dbb1-109">Un [servidor y una base de datos de Azure Database for PostgreSQL](quickstart-create-server-database-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="0dbb1-109">An [Azure Database for PostgreSQL server and database](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="0dbb1-110">Instalar [CLI de Azure 2.0](/cli/azure/install-azure-cli) línea de comandos utilidad o use Hola Shell en la nube de Azure en el Explorador de Hola.</span><span class="sxs-lookup"><span data-stu-id="0dbb1-110">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command line utility or use hello Azure Cloud Shell in hello browser.</span></span>

## <a name="configure-firewall-rules-for-azure-database-for-postgresql"></a><span data-ttu-id="0dbb1-111">Configuración de reglas de firewall para Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="0dbb1-111">Configure firewall rules for Azure Database for PostgreSQL</span></span>
<span data-ttu-id="0dbb1-112">Hola [az postgres servidor regla de firewall](/cli/azure/postgres/server/firewall-rule) comandos son tooconfigure usa reglas de firewall.</span><span class="sxs-lookup"><span data-stu-id="0dbb1-112">hello [az postgres server firewall-rule](/cli/azure/postgres/server/firewall-rule) commands are used tooconfigure firewall rules.</span></span>

## <a name="list-firewall-rules"></a><span data-ttu-id="0dbb1-113">Enumerar reglas de firewall</span><span class="sxs-lookup"><span data-stu-id="0dbb1-113">List firewall rules</span></span> 
<span data-ttu-id="0dbb1-114">toolist Hola existente de reglas de firewall de servidor en el servidor de hello, ejecute hello [lista de regla de firewall del servidor de az postgres](/cli/azure/postgres/server/firewall-rule#list) comando.</span><span class="sxs-lookup"><span data-stu-id="0dbb1-114">toolist hello existing server firewall rules on hello server, run hello [az postgres server firewall-rule list](/cli/azure/postgres/server/firewall-rule#list) command.</span></span>
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401
```
<span data-ttu-id="0dbb1-115">salida de Hello enumera las reglas de hello si los hay, de forma predeterminada en JSON de formato.</span><span class="sxs-lookup"><span data-stu-id="0dbb1-115">hello output lists hello rules if any, by default in JSON format.</span></span> <span data-ttu-id="0dbb1-116">Puede usar el modificador de hello `--output table` para un formato más legible de la tabla como resultado de hello.</span><span class="sxs-lookup"><span data-stu-id="0dbb1-116">You may use hello switch `--output table` for a more readable table format as hello output.</span></span>
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401 --output table
```
## <a name="create-firewall-rule"></a><span data-ttu-id="0dbb1-117">Crear reglas de firewall</span><span class="sxs-lookup"><span data-stu-id="0dbb1-117">Create firewall rule</span></span>
<span data-ttu-id="0dbb1-118">una nueva regla de firewall en servidor de hello, ejecute hello toocreate [crear az postgres servidor regla de firewall](/cli/azure/postgres/server/firewall-rule#create) comando.</span><span class="sxs-lookup"><span data-stu-id="0dbb1-118">toocreate a new firewall rule on hello server, run hello [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> 

<span data-ttu-id="0dbb1-119">Este ejemplo permite una serie de todos los servidores de Hola de tooaccess de direcciones IP **mypgserver 20170401.postgres.database.azure.com**</span><span class="sxs-lookup"><span data-stu-id="0dbb1-119">This example allows a range of all IP addresses tooaccess hello server **mypgserver-20170401.postgres.database.azure.com**</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
<span data-ttu-id="0dbb1-120">tooallow una tooaccess de dirección IP singular, proporcionar Hola la misma dirección como Hola IP inicial y final de IP, como en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="0dbb1-120">tooallow a singular IP address tooaccess, provide hello same address as hello Start IP and End IP, as in this example.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  
--server mypgserver-20170401 --name "AllowSingleIpAddress" --start-ip-address 13.83.152.1 --end-ip-address 13.83.152.1
```
<span data-ttu-id="0dbb1-121">Cuando se realiza correctamente, el resultado del comando de hello muestra detalles de Hola Hola de regla de firewall que ha creado, de forma predeterminada en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="0dbb1-121">Upon success, hello command output lists hello details of hello firewall rule you have created, by default in JSON format.</span></span> <span data-ttu-id="0dbb1-122">Si se produce un error, Hola había salida showserror texto del mensaje en su lugar.</span><span class="sxs-lookup"><span data-stu-id="0dbb1-122">If there is a failure, hello output showserror message text instead.</span></span>

## <a name="update-firewall-rule"></a><span data-ttu-id="0dbb1-123">Actualizar reglas de firewall</span><span class="sxs-lookup"><span data-stu-id="0dbb1-123">Update firewall rule</span></span> 
<span data-ttu-id="0dbb1-124">Actualizar una regla de firewall existente sobre el uso de servidor de hello [actualización de regla de firewall de servidor de az postgres](/cli/azure/postgres/server/firewall-rule#update) comando.</span><span class="sxs-lookup"><span data-stu-id="0dbb1-124">Update an existing firewall rule on hello server using [az postgres server firewall-rule update](/cli/azure/postgres/server/firewall-rule#update) command.</span></span> <span data-ttu-id="0dbb1-125">Proporcione el nombre de Hola de regla de firewall existente hello como entrada y Hola inicio IP y final IP atributos tooupdate.</span><span class="sxs-lookup"><span data-stu-id="0dbb1-125">Provide hello name of hello existing firewall rule as input, and hello start IP and end IP attributes tooupdate.</span></span>
```azurecli-interactive
az postgres server firewall-rule update --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.255
```
<span data-ttu-id="0dbb1-126">Cuando se realiza correctamente, el resultado del comando de hello muestra detalles de Hola Hola de regla de firewall que ha actualizado, de forma predeterminada en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="0dbb1-126">Upon success, hello command output lists hello details of hello firewall rule you have updated, by default in JSON format.</span></span> <span data-ttu-id="0dbb1-127">Si se produce un error, Hola había salida showserror texto del mensaje en su lugar.</span><span class="sxs-lookup"><span data-stu-id="0dbb1-127">If there is a failure, hello output showserror message text instead.</span></span>
> [!NOTE]
> <span data-ttu-id="0dbb1-128">Si la regla de firewall de hello no existe, se crea mediante el comando de actualización de Hola.</span><span class="sxs-lookup"><span data-stu-id="0dbb1-128">If hello firewall rule does not exist, it gets created by hello update command.</span></span>

## <a name="show-firewall-rule-details"></a><span data-ttu-id="0dbb1-129">Mostrar los detalles de la regla de firewall</span><span class="sxs-lookup"><span data-stu-id="0dbb1-129">Show firewall rule details</span></span>
<span data-ttu-id="0dbb1-130">También puede mostrar detalles de la regla para un servidor de firewall existente Hola ejecutando [demostración de regla de firewall de servidor de az postgres](/cli/azure/postgres/server/firewall-rule#show) comando.</span><span class="sxs-lookup"><span data-stu-id="0dbb1-130">You can also show hello existing firewall rule details for a server by running [az postgres server firewall-rule show](/cli/azure/postgres/server/firewall-rule#show) command.</span></span>
```azurecli-interactive
az postgres server firewall-rule show --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
<span data-ttu-id="0dbb1-131">Cuando se realiza correctamente, el resultado del comando de hello muestra detalles de Hola Hola de regla de firewall que ha especificado, de forma predeterminada en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="0dbb1-131">Upon success, hello command output lists hello details of hello firewall rule you have specified, by default in JSON format.</span></span> <span data-ttu-id="0dbb1-132">Si se produce un error, Hola había salida showserror texto del mensaje en su lugar.</span><span class="sxs-lookup"><span data-stu-id="0dbb1-132">If there is a failure, hello output showserror message text instead.</span></span>

## <a name="delete-firewall-rule"></a><span data-ttu-id="0dbb1-133">Eliminar reglas de firewall</span><span class="sxs-lookup"><span data-stu-id="0dbb1-133">Delete firewall rule</span></span>
<span data-ttu-id="0dbb1-134">acceso de toorevoke para un intervalo IP del servidor de hello, eliminar una regla de firewall existente mediante la ejecución de hello [eliminar az postgres servidor regla de firewall](/cli/azure/postgres/server/firewall-rule#delete) comando.</span><span class="sxs-lookup"><span data-stu-id="0dbb1-134">toorevoke access for an IP range from hello server, delete an existing firewall rule by executing hello [az postgres server firewall-rule delete](/cli/azure/postgres/server/firewall-rule#delete) command.</span></span> <span data-ttu-id="0dbb1-135">Proporcione el nombre de Hola Hola existente de regla de firewall.</span><span class="sxs-lookup"><span data-stu-id="0dbb1-135">Provide hello name of hello existing firewall rule.</span></span>
```azurecli-interactive
az postgres server firewall-rule delete --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
<span data-ttu-id="0dbb1-136">Cuando se realiza correctamente, no hay ninguna salida.</span><span class="sxs-lookup"><span data-stu-id="0dbb1-136">Upon success, there is no output.</span></span> <span data-ttu-id="0dbb1-137">En caso de error, se devuelve el texto del mensaje de error de Hola.</span><span class="sxs-lookup"><span data-stu-id="0dbb1-137">Upon failure, hello error message text is returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0dbb1-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0dbb1-138">Next steps</span></span>
- <span data-ttu-id="0dbb1-139">De forma similar, puede utilizar un explorador web demasiado[crear y administrar la base de datos PostgreSQL las reglas de firewall mediante Hola portal de Azure](howto-manage-firewall-using-portal.md)</span><span class="sxs-lookup"><span data-stu-id="0dbb1-139">Similarly, you can use a web browser too[Create and manage Azure Database for PostgreSQL firewall rules using hello Azure portal](howto-manage-firewall-using-portal.md)</span></span>
- <span data-ttu-id="0dbb1-140">Para más información, consulte [Reglas de firewall de servidor de Azure Database for PostgreSQL](concepts-firewall-rules.md).</span><span class="sxs-lookup"><span data-stu-id="0dbb1-140">Understand more about [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md)</span></span>
- <span data-ttu-id="0dbb1-141">Para obtener ayuda sobre conexión tooan base de datos de Azure para PostgreSQL server, vea [bibliotecas de conexiones de base de datos de PostgreSQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="0dbb1-141">For help in connecting tooan Azure Database for PostgreSQL server, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
