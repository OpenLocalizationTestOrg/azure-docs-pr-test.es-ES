---
title: "parámetros de servicio de hello aaaConfigure en la base de datos de Azure para PostgreSQL | Documentos de Microsoft"
description: "Este artículo describe cómo tooconfigure parámetros de servicio de hello en la base de datos de Azure para usar PostgreSQL Hola línea de comandos de CLI de Azure."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 84a11de24ba87fc0eb6744aaa4b53f65a183903d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="customize-server-configuration-parameters-using-azure-cli"></a><span data-ttu-id="a2c3b-103">Personalización de los parámetros de configuración del servidor con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="a2c3b-103">Customize server configuration parameters using Azure CLI</span></span>
<span data-ttu-id="a2c3b-104">Puede enumerar, mostrar y actualizar los parámetros de configuración para un servidor de Azure PostgreSQL utilizando Hola interfaz de línea de comandos (CLI de Azure).</span><span class="sxs-lookup"><span data-stu-id="a2c3b-104">You can list, show and update configuration parameters for an Azure PostgreSQL server using hello Command Line Interface (Azure CLI).</span></span> <span data-ttu-id="a2c3b-105">Sin embargo, en el nivel del servidor, solo se expone y se puede modificar un subconjunto de las opciones de configuración del motor.</span><span class="sxs-lookup"><span data-stu-id="a2c3b-105">However, only a subset of engine configurations are exposed at server-level and can be modified.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a2c3b-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a2c3b-106">Prerequisites</span></span>
<span data-ttu-id="a2c3b-107">toostep a través de este tooguide cómo, necesita:</span><span class="sxs-lookup"><span data-stu-id="a2c3b-107">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="a2c3b-108">Un servidor y una base de datos [Creación de una instancia de Azure Database for PostgreSQL](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="a2c3b-108">A server and database [Create an Azure Database for PostgreSQL](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="a2c3b-109">Instalar [CLI de Azure 2.0](/cli/azure/install-azure-cli) línea de comandos utilidad o use Hola Shell en la nube de Azure en el Explorador de Hola.</span><span class="sxs-lookup"><span data-stu-id="a2c3b-109">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command line utility or use hello Azure Cloud Shell in hello browser.</span></span>

## <a name="list-server-configuration-parameters-for-azure-database-for-postgresql-server"></a><span data-ttu-id="a2c3b-110">Lista de los parámetros de configuración del servidor de Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="a2c3b-110">List server configuration parameters for Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="a2c3b-111">toolist todos los parámetros modificables en un servidor y sus valores, ejecute hello [lista de configuración de servidores de az postgres](/cli/azure/postgres/server/configuration#list) comando.</span><span class="sxs-lookup"><span data-stu-id="a2c3b-111">toolist all modifiable parameters in a server and their values, run hello [az postgres server configuration list](/cli/azure/postgres/server/configuration#list) command.</span></span>

<span data-ttu-id="a2c3b-112">Puede enumerar los parámetros de configuración de servidor de Hola para servidor hello **mypgserver 20170401.postgres.database.azure.com** en el grupo de recursos **myresourcegroup**.</span><span class="sxs-lookup"><span data-stu-id="a2c3b-112">You can list hello server configuration parameters for hello server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup**.</span></span>
```azurecli-interactive
az postgres server configuration list --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="show-server-configuration-parameter-details"></a><span data-ttu-id="a2c3b-113">Presentación de los detalles de los parámetros de configuración del servidor</span><span class="sxs-lookup"><span data-stu-id="a2c3b-113">Show server configuration parameter details</span></span>
<span data-ttu-id="a2c3b-114">detalles de tooshow sobre un parámetro de configuración específica para un servidor, ejecute hello [mostrar de configuración de servidor de az postgres](/cli/azure/postgres/server/configuration#show) comando.</span><span class="sxs-lookup"><span data-stu-id="a2c3b-114">tooshow details about a particular configuration parameter for a server, run hello [az postgres server configuration show](/cli/azure/postgres/server/configuration#show)  command.</span></span>

<span data-ttu-id="a2c3b-115">Este ejemplo muestra detalles de hello **registro\_min\_mensajes** parámetro de configuración de servidor para el servidor **mypgserver 20170401.postgres.database.azure.com** en grupo de recursos **myresourcegroup.**</span><span class="sxs-lookup"><span data-stu-id="a2c3b-115">This example shows details of hello **log\_min\_messages** server configuration parameter for server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup.**</span></span>
```azurecli-interactive
az postgres server configuration show --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="modify-server-configuration-parameter-value"></a><span data-ttu-id="a2c3b-116">Modificación del valor de los parámetros de configuración del servidor</span><span class="sxs-lookup"><span data-stu-id="a2c3b-116">Modify server configuration parameter value</span></span>
<span data-ttu-id="a2c3b-117">También puede modificar el valor de Hola de ciertos parámetros de configuración de servidor y se actualizará el valor de configuración subyacente Hola Hola PostgreSQL motor de server.</span><span class="sxs-lookup"><span data-stu-id="a2c3b-117">You can also modify hello value of a certain server configuration parameter, and this updates hello underlying configuration value for hello PostgreSQL server engine.</span></span> <span data-ttu-id="a2c3b-118">Hola de uso de configuración de hello tooupdate [conjunto de configuración de servidor de az postgres](/cli/azure/postgres/server/configuration#set) comando.</span><span class="sxs-lookup"><span data-stu-id="a2c3b-118">tooupdate hello configuration use hello [az postgres server configuration set](/cli/azure/postgres/server/configuration#set) command.</span></span> 

<span data-ttu-id="a2c3b-119">Hola tooupdate **registro\_min\_mensajes** parámetro de configuración de servidor del servidor de **mypgserver 20170401.postgres.database.azure.com** bajo el grupo de recursos **myresourcegroup.**</span><span class="sxs-lookup"><span data-stu-id="a2c3b-119">tooupdate hello **log\_min\_messages** server configuration parameter of server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup.**</span></span>
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401 --value INFO
```
<span data-ttu-id="a2c3b-120">Si desea que el valor de hello tooreset de un parámetro de configuración, simplemente elija tooleave out Hola opcional `--value` parámetro y el servicio de Hola aplicarán el valor predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="a2c3b-120">If you want tooreset hello value of a configuration parameter, you simply choose tooleave out hello optional `--value` parameter, and hello service will apply hello default value.</span></span> <span data-ttu-id="a2c3b-121">En el ejemplo anterior, sería:</span><span class="sxs-lookup"><span data-stu-id="a2c3b-121">In above example, it would look like:</span></span>
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
<span data-ttu-id="a2c3b-122">Se restablecerá hello **registro\_min\_mensajes** valor predeterminado de configuración toohello **advertencia**.</span><span class="sxs-lookup"><span data-stu-id="a2c3b-122">This will reset hello **log\_min\_messages** configuration toohello default value **WARNING**.</span></span> <span data-ttu-id="a2c3b-123">Para más información sobre la configuración del servidor y los valores permitidos, consulte la documentación de PostgreSQL en [Server Configuration](https://www.postgresql.org/docs/9.6/static/runtime-config.html) (Configuración del servidor).</span><span class="sxs-lookup"><span data-stu-id="a2c3b-123">For further details on server configuration and permissible values, see PostgreSQL documentation on [Server Configuration](https://www.postgresql.org/docs/9.6/static/runtime-config.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2c3b-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a2c3b-124">Next steps</span></span>
- <span data-ttu-id="a2c3b-125">registros del servidor de acceso y tooconfigure, consulte [registros del servidor de base de datos de PostgreSQL](concepts-server-logs.md)</span><span class="sxs-lookup"><span data-stu-id="a2c3b-125">tooconfigure and access server logs, see [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md)</span></span>
