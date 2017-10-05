---
title: "Configuración de los parámetros del servicio en Azure Database para PostgreSQL | Microsoft Docs"
description: "En este artículo se describe cómo configurar los parámetros de servicio de Azure Database for PostgreSQL mediante la línea de comandos de la CLI de Azure."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: c8a3b5a0225c2cede180d8d57681f2e1a6c6cc3a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="customize-server-configuration-parameters-using-azure-cli"></a><span data-ttu-id="7912b-103">Personalización de los parámetros de configuración del servidor con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="7912b-103">Customize server configuration parameters using Azure CLI</span></span>
<span data-ttu-id="7912b-104">Puede enumerar, mostrar y actualizar los parámetros de configuración de un servidor de Azure PostgreSQL con la interfaz de la línea de comandos (CLI de Azure).</span><span class="sxs-lookup"><span data-stu-id="7912b-104">You can list, show and update configuration parameters for an Azure PostgreSQL server using the Command Line Interface (Azure CLI).</span></span> <span data-ttu-id="7912b-105">Sin embargo, en el nivel del servidor, solo se expone y se puede modificar un subconjunto de las opciones de configuración del motor.</span><span class="sxs-lookup"><span data-stu-id="7912b-105">However, only a subset of engine configurations are exposed at server-level and can be modified.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="7912b-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7912b-106">Prerequisites</span></span>
<span data-ttu-id="7912b-107">Para seguir esta guía, necesitará:</span><span class="sxs-lookup"><span data-stu-id="7912b-107">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="7912b-108">Un servidor y una base de datos [Creación de una instancia de Azure Database for PostgreSQL](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="7912b-108">A server and database [Create an Azure Database for PostgreSQL](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="7912b-109">Instale la utilidad de línea de comandos [CLI de Azure 2.0](/cli/azure/install-azure-cli) o use Azure Cloud Shell en el explorador.</span><span class="sxs-lookup"><span data-stu-id="7912b-109">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command line utility or use the Azure Cloud Shell in the browser.</span></span>

## <a name="list-server-configuration-parameters-for-azure-database-for-postgresql-server"></a><span data-ttu-id="7912b-110">Lista de los parámetros de configuración del servidor de Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="7912b-110">List server configuration parameters for Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="7912b-111">Para obtener una lista de todos los parámetros modificables en un servidor y sus valores, ejecute el comando [az postgres server configuration list](/cli/azure/postgres/server/configuration#list).</span><span class="sxs-lookup"><span data-stu-id="7912b-111">To list all modifiable parameters in a server and their values, run the [az postgres server configuration list](/cli/azure/postgres/server/configuration#list) command.</span></span>

<span data-ttu-id="7912b-112">Puede enumerar los parámetros de configuración del servidor **mypgserver-20170401.postgres.database.azure.com** en el grupo de recursos **myresourcegroup**.</span><span class="sxs-lookup"><span data-stu-id="7912b-112">You can list the server configuration parameters for the server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup**.</span></span>
```azurecli-interactive
az postgres server configuration list --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="show-server-configuration-parameter-details"></a><span data-ttu-id="7912b-113">Presentación de los detalles de los parámetros de configuración del servidor</span><span class="sxs-lookup"><span data-stu-id="7912b-113">Show server configuration parameter details</span></span>
<span data-ttu-id="7912b-114">Para mostrar los detalles de un parámetro de configuración específico de un servidor, ejecute el comando [az postgres server configuration show](/cli/azure/postgres/server/configuration#show).</span><span class="sxs-lookup"><span data-stu-id="7912b-114">To show details about a particular configuration parameter for a server, run the [az postgres server configuration show](/cli/azure/postgres/server/configuration#show)  command.</span></span>

<span data-ttu-id="7912b-115">En este ejemplo se muestran detalles del parámetro de configuración **log\_min\_messages** del servidor **mypgserver-20170401.postgres.database.azure.com** en el grupo de recursos **myresourcegroup.**</span><span class="sxs-lookup"><span data-stu-id="7912b-115">This example shows details of the **log\_min\_messages** server configuration parameter for server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup.**</span></span>
```azurecli-interactive
az postgres server configuration show --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="modify-server-configuration-parameter-value"></a><span data-ttu-id="7912b-116">Modificación del valor de los parámetros de configuración del servidor</span><span class="sxs-lookup"><span data-stu-id="7912b-116">Modify server configuration parameter value</span></span>
<span data-ttu-id="7912b-117">También puede modificar el valor de un determinado parámetro de configuración del servidor; esta acción actualizará el valor de configuración subyacente del motor del servidor de PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="7912b-117">You can also modify the value of a certain server configuration parameter, and this updates the underlying configuration value for the PostgreSQL server engine.</span></span> <span data-ttu-id="7912b-118">Para actualizar la configuración, use el comando [az postgres server configuration set](/cli/azure/postgres/server/configuration#set).</span><span class="sxs-lookup"><span data-stu-id="7912b-118">To update the configuration use the [az postgres server configuration set](/cli/azure/postgres/server/configuration#set) command.</span></span> 

<span data-ttu-id="7912b-119">Para actualizar el parámetro de configuración **log\_min\_messages** del servidor **mypgserver-20170401.postgres.database.azure.com** en el grupo de recursos **myresourcegroup.**</span><span class="sxs-lookup"><span data-stu-id="7912b-119">To update the **log\_min\_messages** server configuration parameter of server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup.**</span></span>
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401 --value INFO
```
<span data-ttu-id="7912b-120">Si desea restablecer el valor de un parámetro de configuración, basta con no incluir el parámetro opcional `--value` y el servicio aplicará el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="7912b-120">If you want to reset the value of a configuration parameter, you simply choose to leave out the optional `--value` parameter, and the service will apply the default value.</span></span> <span data-ttu-id="7912b-121">En el ejemplo anterior, sería:</span><span class="sxs-lookup"><span data-stu-id="7912b-121">In above example, it would look like:</span></span>
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
<span data-ttu-id="7912b-122">La configuración de **log\_min\_messages** se restablecerá al valor predeterminado **WARNING**.</span><span class="sxs-lookup"><span data-stu-id="7912b-122">This will reset the **log\_min\_messages** configuration to the default value **WARNING**.</span></span> <span data-ttu-id="7912b-123">Para más información sobre la configuración del servidor y los valores permitidos, consulte la documentación de PostgreSQL en [Server Configuration](https://www.postgresql.org/docs/9.6/static/runtime-config.html) (Configuración del servidor).</span><span class="sxs-lookup"><span data-stu-id="7912b-123">For further details on server configuration and permissible values, see PostgreSQL documentation on [Server Configuration](https://www.postgresql.org/docs/9.6/static/runtime-config.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7912b-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7912b-124">Next steps</span></span>
- <span data-ttu-id="7912b-125">Para configurar y obtener acceso a los registros del servidor, consulte [Registros del servidor en Azure Database for PostgreSQL](concepts-server-logs.md).</span><span class="sxs-lookup"><span data-stu-id="7912b-125">To configure and access server logs, see [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md)</span></span>
