---
title: "¿Cómo tooback una copia de seguridad y restaurar un servidor de base de datos de Azure para PostgreSQL | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooback seguridad y restauración de un servidor de base de datos de Azure para PostgreSQL mediante el uso de Hola CLI de Azure."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 0b9ed25e3e3a88dd5c7ffe2ae7c27f8eef9be710
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooback-up-and-restore-a-server-in-azure-database-for-postgresql-by-using-hello-azure-cli"></a><span data-ttu-id="e43a0-103">¿Cómo tooback seguridad y restauración de un servidor de base de datos de Azure para PostgreSQL mediante el uso de Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="e43a0-103">How tooback up and restore a server in Azure Database for PostgreSQL by using hello Azure CLI</span></span>

<span data-ttu-id="e43a0-104">Usar base de datos de Azure para PostgreSQL toorestore un tooan de base de datos del servidor fecha anterior que abarca desde 7 días too35.</span><span class="sxs-lookup"><span data-stu-id="e43a0-104">Use Azure Database for PostgreSQL toorestore a server database tooan earlier date that spans from 7 too35 days.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e43a0-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e43a0-105">Prerequisites</span></span>
<span data-ttu-id="e43a0-106">toocomplete este tooguide cómo, necesita:</span><span class="sxs-lookup"><span data-stu-id="e43a0-106">toocomplete this how-tooguide, you need:</span></span>
- <span data-ttu-id="e43a0-107">Un [servidor y una base de datos de Azure Database for PostgreSQL](quickstart-create-server-database-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="e43a0-107">An [Azure Database for PostgreSQL server and database](quickstart-create-server-database-azure-cli.md)</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

 

> [!IMPORTANT]
> <span data-ttu-id="e43a0-108">Si instala y usar hello CLI de Azure localmente, este tooguide cómo requiere el uso de CLI de Azure versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="e43a0-108">If you install and use hello Azure CLI locally, this how-tooguide requires that you use Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="e43a0-109">versión de hello tooconfirm, en línea de comandos de CLI de Azure de hello, escriba `az --version`.</span><span class="sxs-lookup"><span data-stu-id="e43a0-109">tooconfirm hello version, at hello Azure CLI command prompt, enter `az --version`.</span></span> <span data-ttu-id="e43a0-110">tooinstall o actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e43a0-110">tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="back-up-happens-automatically"></a><span data-ttu-id="e43a0-111">La copia de seguridad se realiza automáticamente</span><span class="sxs-lookup"><span data-stu-id="e43a0-111">Back up happens automatically</span></span>
<span data-ttu-id="e43a0-112">Cuando se usa la base de datos de Azure para PostgreSQL, servicio de base de datos de hello realiza automáticamente una copia de seguridad del servicio de hello cada 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="e43a0-112">When you use Azure Database for PostgreSQL, hello database service automatically makes a backup of hello service every 5 minutes.</span></span> 

<span data-ttu-id="e43a0-113">Para nivel básico, las copias de seguridad de hello estarán disponibles durante 7 días.</span><span class="sxs-lookup"><span data-stu-id="e43a0-113">For Basic Tier, hello backups are available for 7 days.</span></span> <span data-ttu-id="e43a0-114">Para el nivel estándar, las copias de seguridad de hello están disponibles para 35 días.</span><span class="sxs-lookup"><span data-stu-id="e43a0-114">For Standard Tier, hello backups are available for 35 days.</span></span> <span data-ttu-id="e43a0-115">Para más información, consulte el artículo de [planes de tarifa de Azure Database for PostgreSQL](concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="e43a0-115">For more information, see [Azure Database for PostgreSQL pricing tiers](concepts-service-tiers.md).</span></span>

<span data-ttu-id="e43a0-116">Con esta característica de copia de seguridad automática, puede restaurar servidor hello y su bases de datos tooan fecha anterior o al momento dado.</span><span class="sxs-lookup"><span data-stu-id="e43a0-116">With this automatic backup feature, you can restore hello server and its databases tooan earlier date, or point in time.</span></span>

## <a name="restore-a-database-tooa-previous-point-in-time-by-using-hello-azure-cli"></a><span data-ttu-id="e43a0-117">Restaurar un punto anterior de tooa de base de datos en el tiempo mediante Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="e43a0-117">Restore a database tooa previous point in time by using hello Azure CLI</span></span>
<span data-ttu-id="e43a0-118">Base de datos de Azure de uso para PostgreSQL toorestore Hola server tooa punto anterior en el tiempo.</span><span class="sxs-lookup"><span data-stu-id="e43a0-118">Use Azure Database for PostgreSQL toorestore hello server tooa previous point in time.</span></span> <span data-ttu-id="e43a0-119">datos de Hello restaurar están tooa copiado nuevo servidor y servidor existente de Hola se deja tal como está.</span><span class="sxs-lookup"><span data-stu-id="e43a0-119">hello restored data is copied tooa new server, and hello existing server is left as is.</span></span> <span data-ttu-id="e43a0-120">Por ejemplo, si una tabla se elimina accidentalmente a mediodía hoy en día, puede restaurar toohello tiempo justo antes del mediodía.</span><span class="sxs-lookup"><span data-stu-id="e43a0-120">For example, if a table is accidentally dropped at noon today, you can restore toohello time just before noon.</span></span> <span data-ttu-id="e43a0-121">A continuación, puede recuperar Hola falta la tabla y los datos de copia de hello restaurar del servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="e43a0-121">Then, you can retrieve hello missing table and data from hello restored copy of hello server.</span></span> 

<span data-ttu-id="e43a0-122">servidor de hello toorestore, use hello Azure CLI [restauración del servidor postgres az](/cli/azure/postgres/server#restore) comando.</span><span class="sxs-lookup"><span data-stu-id="e43a0-122">toorestore hello server, use hello Azure CLI [az postgres server restore](/cli/azure/postgres/server#restore) command.</span></span>

### <a name="run-hello-restore-command"></a><span data-ttu-id="e43a0-123">Ejecute el comando de restauración de Hola</span><span class="sxs-lookup"><span data-stu-id="e43a0-123">Run hello restore command</span></span>

<span data-ttu-id="e43a0-124">servidor de hello toorestore, en línea de comandos de CLI de Azure de hello, escriba Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e43a0-124">toorestore hello server, at hello Azure CLI command prompt, enter hello following command:</span></span>

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

<span data-ttu-id="e43a0-125">Hola `az postgres server restore` comando requiere Hola parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="e43a0-125">hello `az postgres server restore` command requires hello following parameters:</span></span>
| <span data-ttu-id="e43a0-126">Configuración</span><span class="sxs-lookup"><span data-stu-id="e43a0-126">Setting</span></span> | <span data-ttu-id="e43a0-127">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="e43a0-127">Suggested value</span></span> | <span data-ttu-id="e43a0-128">Descripción</span><span class="sxs-lookup"><span data-stu-id="e43a0-128">Description</span></span>  |
| --- | --- | --- |
| <span data-ttu-id="e43a0-129">resource-group</span><span class="sxs-lookup"><span data-stu-id="e43a0-129">resource-group</span></span> |  <span data-ttu-id="e43a0-130">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e43a0-130">myResourceGroup</span></span> |  <span data-ttu-id="e43a0-131">El grupo de recursos donde existe el servidor de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="e43a0-131">The resource group where hello source server exists.</span></span>  |
| <span data-ttu-id="e43a0-132">name</span><span class="sxs-lookup"><span data-stu-id="e43a0-132">name</span></span> | <span data-ttu-id="e43a0-133">mypgserver-restored</span><span class="sxs-lookup"><span data-stu-id="e43a0-133">mypgserver-restored</span></span> | <span data-ttu-id="e43a0-134">nombre de Hola de hello nuevo servidor que se crea mediante el comando de restauración de Hola.</span><span class="sxs-lookup"><span data-stu-id="e43a0-134">hello name of hello new server that is created by hello restore command.</span></span> |
| <span data-ttu-id="e43a0-135">restore-point-in-time</span><span class="sxs-lookup"><span data-stu-id="e43a0-135">restore-point-in-time</span></span> | <span data-ttu-id="e43a0-136">2017-04-13T13:59:00Z</span><span class="sxs-lookup"><span data-stu-id="e43a0-136">2017-04-13T13:59:00Z</span></span> | <span data-ttu-id="e43a0-137">Seleccione un punto de tiempo toorestore a.</span><span class="sxs-lookup"><span data-stu-id="e43a0-137">Select a point in time toorestore to.</span></span> <span data-ttu-id="e43a0-138">Esta fecha y hora deben estar dentro de hello del servidor de origen período de retención de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="e43a0-138">This date and time must be within hello source server's back up retention period.</span></span> <span data-ttu-id="e43a0-139">Utilice el formato de fecha y hora de hello ISO8601.</span><span class="sxs-lookup"><span data-stu-id="e43a0-139">Use hello ISO8601 date and time format.</span></span> <span data-ttu-id="e43a0-140">Por ejemplo, puede usar su propia zona horaria, como `2017-04-13T05:59:00-08:00`.</span><span class="sxs-lookup"><span data-stu-id="e43a0-140">For example, you can use your own local time zone, such as `2017-04-13T05:59:00-08:00`.</span></span> <span data-ttu-id="e43a0-141">También puede usar Hola formato UTC Zulú, por ejemplo, `2017-04-13T13:59:00Z`.</span><span class="sxs-lookup"><span data-stu-id="e43a0-141">You can also use hello UTC Zulu format, for example, `2017-04-13T13:59:00Z`.</span></span> |
| <span data-ttu-id="e43a0-142">source-server</span><span class="sxs-lookup"><span data-stu-id="e43a0-142">source-server</span></span> | <span data-ttu-id="e43a0-143">mypgserver-20170401</span><span class="sxs-lookup"><span data-stu-id="e43a0-143">mypgserver-20170401</span></span> | <span data-ttu-id="e43a0-144">nombre de Hola o Id. de hello toorestore de servidor de origen de.</span><span class="sxs-lookup"><span data-stu-id="e43a0-144">hello name or ID of hello source server toorestore from.</span></span> |

<span data-ttu-id="e43a0-145">Al restaurar un servidor tooan punto anterior en el tiempo, se crea un nuevo servidor.</span><span class="sxs-lookup"><span data-stu-id="e43a0-145">When you restore a server tooan earlier point in time, a new server is created.</span></span> <span data-ttu-id="e43a0-146">servidor original de Hola y sus bases de datos de hello especifican punto en el tiempo son toohello copiado nuevo servidor.</span><span class="sxs-lookup"><span data-stu-id="e43a0-146">hello original server and its databases from hello specified point in time are copied toohello new server.</span></span>

<span data-ttu-id="e43a0-147">los valores de nivel de ubicación y el precio de Hola para servidor hello restaurado permanecen Hola mismo como servidor de hello original.</span><span class="sxs-lookup"><span data-stu-id="e43a0-147">hello location and pricing tier values for hello restored server remain hello same as hello original server.</span></span> 

<span data-ttu-id="e43a0-148">Hola `az postgres server restore` comando es sincrónico.</span><span class="sxs-lookup"><span data-stu-id="e43a0-148">hello `az postgres server restore` command is synchronous.</span></span> <span data-ttu-id="e43a0-149">Después de restaura el servidor de hello, utilizarla nuevo proceso de hello toorepeat para otro punto en el tiempo.</span><span class="sxs-lookup"><span data-stu-id="e43a0-149">After hello server is restored, you can use it again toorepeat hello process for a different point in time.</span></span> 

<span data-ttu-id="e43a0-150">Después de hello restaurar proceso finaliza, busque el nuevo servidor de Hola y comprobar que se ha restaurado datos Hola según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="e43a0-150">After hello restore process finishes, locate hello new server and verify that hello data is restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e43a0-151">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e43a0-151">Next steps</span></span>
[<span data-ttu-id="e43a0-152">Bibliotecas de conexiones de Azure Database para PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="e43a0-152">Connection libraries for Azure Database for PostgreSQL</span></span>](concepts-connection-libraries.md)
