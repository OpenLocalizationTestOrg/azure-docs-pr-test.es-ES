---
title: "Configuración y acceso a los registros del servidor para PostgreSQL con la CLI de Azure | Microsoft Docs"
description: "En este artículo se describe cómo configurar los registros de servidor de Azure Database for PostgreSQL, y obtener acceso a ellos, mediante la línea de comandos de la CLI de Azure."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 26f8e12c493904f722cad5191ee053feff20f7fc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="configure-and-access-server-logs-using-azure-cli"></a><span data-ttu-id="9d41b-103">Configuración y acceso a los registros del servidor con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="9d41b-103">Configure and access server logs using Azure CLI</span></span>
<span data-ttu-id="9d41b-104">Puede descargar los registros de error del servidor de PostgreSQL mediante la interfaz de la línea de comandos (CLI de Azure).</span><span class="sxs-lookup"><span data-stu-id="9d41b-104">You can download the PostgreSQL server error logs using the Command Line Interface (Azure CLI).</span></span> <span data-ttu-id="9d41b-105">Sin embargo, no se admite el acceso a los registros de transacciones.</span><span class="sxs-lookup"><span data-stu-id="9d41b-105">However, access to transaction logs is not supported.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9d41b-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9d41b-106">Prerequisites</span></span>
<span data-ttu-id="9d41b-107">Para seguir esta guía, necesitará:</span><span class="sxs-lookup"><span data-stu-id="9d41b-107">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="9d41b-108">Un [servidor de Azure Database for PostgreSQL](quickstart-create-server-database-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="9d41b-108">An [Azure Database for PostgreSQL server](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="9d41b-109">Instale la utilidad de línea de comandos [CLI de Azure 2.0](/cli/azure/install-azure-cli) o use Azure Cloud Shell en el explorador.</span><span class="sxs-lookup"><span data-stu-id="9d41b-109">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command-line utility or use the Azure Cloud Shell in the browser.</span></span>

## <a name="configure-logging-for-azure-database-for-postgresql"></a><span data-ttu-id="9d41b-110">Configuración del registro para Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="9d41b-110">Configure logging for Azure Database for PostgreSQL</span></span>
<span data-ttu-id="9d41b-111">Puede configurar el servidor para tener acceso a los registros de consulta y los registros de error.</span><span class="sxs-lookup"><span data-stu-id="9d41b-111">You can configure the server to access query logs and error logs.</span></span> <span data-ttu-id="9d41b-112">Los registros de error pueden contener información de vaciado automático, conexión y puntos de comprobación.</span><span class="sxs-lookup"><span data-stu-id="9d41b-112">Error logs can contain auto-vacuum, connection, and checkpoints information.</span></span>
1. <span data-ttu-id="9d41b-113">Active el registro.</span><span class="sxs-lookup"><span data-stu-id="9d41b-113">Turn on logging</span></span>
2. <span data-ttu-id="9d41b-114">Actualice los valores de log\_statement y log\_min\_duration\_statement para habilitar el registro de consultas.</span><span class="sxs-lookup"><span data-stu-id="9d41b-114">Update log\_statement and log\_min\_duration\_statement to enable query logging</span></span>
3. <span data-ttu-id="9d41b-115">Actualice el período de retención.</span><span class="sxs-lookup"><span data-stu-id="9d41b-115">Update retention period</span></span>

<span data-ttu-id="9d41b-116">Consulte cómo [personalizar los parámetros de configuración del servidor](howto-configure-server-parameters-using-cli.md) para más información.</span><span class="sxs-lookup"><span data-stu-id="9d41b-116">For more information, see [customizing server configuration parameters](howto-configure-server-parameters-using-cli.md).</span></span>

## <a name="list-logs-for-azure-database-for-postgresql-server"></a><span data-ttu-id="9d41b-117">Enumeración de registros del servidor de Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="9d41b-117">List logs for Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="9d41b-118">Para mostrar la lista de archivos de registro disponibles para el servidor, ejecute el comando [az postgres server-logs list](/cli/azure/postgres/server-logs#list).</span><span class="sxs-lookup"><span data-stu-id="9d41b-118">To list the available log files for your server, run the [az postgres server-logs list](/cli/azure/postgres/server-logs#list) command.</span></span>

<span data-ttu-id="9d41b-119">Puede enumerar los archivos de registro del servidor **mypgserver.postgres.database.azure.com** en el grupo de recursos **myresourcegroup**, y dirigirlo a un archivo de texto denominado **log\_files\_list.txt.**</span><span class="sxs-lookup"><span data-stu-id="9d41b-119">You can list the log files for server **mypgserver-20170401.postgres.database.azure.com** under Resource Group **myresourcegroup**, and direct it to a text file called **log\_files\_list.txt.**</span></span>
```azurecli-interactive
az postgres server-logs list --resource-group myresourcegroup --server mypgserver-20170401 > log_files_list.txt
```
## <a name="download-logs-locally-from-the-server"></a><span data-ttu-id="9d41b-120">Descarga de registros del servidor en el sistema local</span><span class="sxs-lookup"><span data-stu-id="9d41b-120">Download logs locally from the server</span></span>
<span data-ttu-id="9d41b-121">El comando [az postgres server-logs download](/cli/azure/postgres/server-logs#download) le permite descargar archivos de registro individuales para su servidor.</span><span class="sxs-lookup"><span data-stu-id="9d41b-121">The [az postgres server-logs download](/cli/azure/postgres/server-logs#download) command allows you to download individual log files for your server.</span></span> 

<span data-ttu-id="9d41b-122">En este ejemplo se descarga el archivo de registro específico para el servidor **mypgserver-20170401.postgres.database.azure.com** en el grupo de recursos **myresourcegroup** a su entorno local.</span><span class="sxs-lookup"><span data-stu-id="9d41b-122">This example downloads the specific log file for the server **mypgserver-20170401.postgres.database.azure.com** under Resource Group **myresourcegroup** to your local environment.</span></span>
```azurecli-interactive
az postgres server-logs download --name 20170414-mypgserver-20170401-postgresql.log --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="next-steps"></a><span data-ttu-id="9d41b-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9d41b-123">Next steps</span></span>
- <span data-ttu-id="9d41b-124">Para más información acerca de los registros del servidor, consulte [Registros del servidor en Azure Database for PostgreSQL](concepts-server-logs.md).</span><span class="sxs-lookup"><span data-stu-id="9d41b-124">To learn more about server logs, see [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md)</span></span>
- <span data-ttu-id="9d41b-125">Para más información sobre los parámetros del servidor, consulte cómo [personalizar los parámetros de configuración del servidor mediante la CLI de Azure](howto-configure-server-parameters-using-cli.md).</span><span class="sxs-lookup"><span data-stu-id="9d41b-125">For more information on server parameters, see [Customize server configuration parameters using Azure CLI](howto-configure-server-parameters-using-cli.md)</span></span>
