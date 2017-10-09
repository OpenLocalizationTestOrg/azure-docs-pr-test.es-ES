---
title: registros del servidor aaaConfigure y acceso para PostgreSQL con CLI de Azure | Documentos de Microsoft
description: "Este artículo describe cómo los registros del servidor hello tooconfigure y acceso en base de datos de Azure para PostgreSQL mediante la línea de comandos de CLI de Azure."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 924d4e7634cc48405bcb0f813cf61d8b72ad8aa0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-access-server-logs-using-azure-cli"></a><span data-ttu-id="782e6-103">Configuración y acceso a los registros del servidor con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="782e6-103">Configure and access server logs using Azure CLI</span></span>
<span data-ttu-id="782e6-104">Puede descargar los registros de errores de servidor hello PostgreSQL mediante Hola interfaz de línea de comandos (CLI de Azure).</span><span class="sxs-lookup"><span data-stu-id="782e6-104">You can download hello PostgreSQL server error logs using hello Command Line Interface (Azure CLI).</span></span> <span data-ttu-id="782e6-105">Sin embargo, no se admite el acceso tootransaction registros.</span><span class="sxs-lookup"><span data-stu-id="782e6-105">However, access tootransaction logs is not supported.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="782e6-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="782e6-106">Prerequisites</span></span>
<span data-ttu-id="782e6-107">toostep a través de este tooguide cómo, necesita:</span><span class="sxs-lookup"><span data-stu-id="782e6-107">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="782e6-108">Un [servidor de Azure Database for PostgreSQL](quickstart-create-server-database-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="782e6-108">An [Azure Database for PostgreSQL server](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="782e6-109">Instalar [CLI de Azure 2.0](/cli/azure/install-azure-cli) de línea de comandos Hola de utilidad o use el Shell de nube de Azure en Explorador de Hola.</span><span class="sxs-lookup"><span data-stu-id="782e6-109">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command-line utility or use hello Azure Cloud Shell in hello browser.</span></span>

## <a name="configure-logging-for-azure-database-for-postgresql"></a><span data-ttu-id="782e6-110">Configuración del registro para Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="782e6-110">Configure logging for Azure Database for PostgreSQL</span></span>
<span data-ttu-id="782e6-111">Puede configurar registros de consultas de hello server tooaccess y registros de errores.</span><span class="sxs-lookup"><span data-stu-id="782e6-111">You can configure hello server tooaccess query logs and error logs.</span></span> <span data-ttu-id="782e6-112">Los registros de error pueden contener información de vaciado automático, conexión y puntos de comprobación.</span><span class="sxs-lookup"><span data-stu-id="782e6-112">Error logs can contain auto-vacuum, connection, and checkpoints information.</span></span>
1. <span data-ttu-id="782e6-113">Active el registro.</span><span class="sxs-lookup"><span data-stu-id="782e6-113">Turn on logging</span></span>
2. <span data-ttu-id="782e6-114">Registro de actualización\_instrucción y registro\_min\_duración\_registro de consultas de instrucción tooenable</span><span class="sxs-lookup"><span data-stu-id="782e6-114">Update log\_statement and log\_min\_duration\_statement tooenable query logging</span></span>
3. <span data-ttu-id="782e6-115">Actualice el período de retención.</span><span class="sxs-lookup"><span data-stu-id="782e6-115">Update retention period</span></span>

<span data-ttu-id="782e6-116">Consulte cómo [personalizar los parámetros de configuración del servidor](howto-configure-server-parameters-using-cli.md) para más información.</span><span class="sxs-lookup"><span data-stu-id="782e6-116">For more information, see [customizing server configuration parameters](howto-configure-server-parameters-using-cli.md).</span></span>

## <a name="list-logs-for-azure-database-for-postgresql-server"></a><span data-ttu-id="782e6-117">Enumeración de registros del servidor de Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="782e6-117">List logs for Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="782e6-118">archivos de registro disponibles toolist hello para el servidor, ejecute hello [lista de registros de servidor postgres az](/cli/azure/postgres/server-logs#list) comando.</span><span class="sxs-lookup"><span data-stu-id="782e6-118">toolist hello available log files for your server, run hello [az postgres server-logs list](/cli/azure/postgres/server-logs#list) command.</span></span>

<span data-ttu-id="782e6-119">Puede enumerar los archivos de registro de hello de servidor **mypgserver 20170401.postgres.database.azure.com** en el grupo de recursos **myresourcegroup**y dirigir tooa texto archivo denominado **registro\_archivos\_list.txt.**</span><span class="sxs-lookup"><span data-stu-id="782e6-119">You can list hello log files for server **mypgserver-20170401.postgres.database.azure.com** under Resource Group **myresourcegroup**, and direct it tooa text file called **log\_files\_list.txt.**</span></span>
```azurecli-interactive
az postgres server-logs list --resource-group myresourcegroup --server mypgserver-20170401 > log_files_list.txt
```
## <a name="download-logs-locally-from-hello-server"></a><span data-ttu-id="782e6-120">Descargar los registros localmente desde el servidor de Hola</span><span class="sxs-lookup"><span data-stu-id="782e6-120">Download logs locally from hello server</span></span>
<span data-ttu-id="782e6-121">Hola [descargar registros de servidor postgres az](/cli/azure/postgres/server-logs#download) comando permite toodownload distintos archivos de registro para el servidor.</span><span class="sxs-lookup"><span data-stu-id="782e6-121">hello [az postgres server-logs download](/cli/azure/postgres/server-logs#download) command allows you toodownload individual log files for your server.</span></span> 

<span data-ttu-id="782e6-122">En este ejemplo Hola de descargas de archivo de registro específico para el servidor de hello **mypgserver 20170401.postgres.database.azure.com** en el grupo de recursos **myresourcegroup** tooyour de entorno local.</span><span class="sxs-lookup"><span data-stu-id="782e6-122">This example downloads hello specific log file for hello server **mypgserver-20170401.postgres.database.azure.com** under Resource Group **myresourcegroup** tooyour local environment.</span></span>
```azurecli-interactive
az postgres server-logs download --name 20170414-mypgserver-20170401-postgresql.log --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="next-steps"></a><span data-ttu-id="782e6-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="782e6-123">Next steps</span></span>
- <span data-ttu-id="782e6-124">toolearn más información acerca de los registros del servidor, consulte [registros del servidor de base de datos de PostgreSQL](concepts-server-logs.md)</span><span class="sxs-lookup"><span data-stu-id="782e6-124">toolearn more about server logs, see [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md)</span></span>
- <span data-ttu-id="782e6-125">Para más información sobre los parámetros del servidor, consulte cómo [personalizar los parámetros de configuración del servidor mediante la CLI de Azure](howto-configure-server-parameters-using-cli.md).</span><span class="sxs-lookup"><span data-stu-id="782e6-125">For more information on server parameters, see [Customize server configuration parameters using Azure CLI](howto-configure-server-parameters-using-cli.md)</span></span>
