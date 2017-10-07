---
title: 'aaa "CLI de Azure Script: crear una base de datos de Azure para PostgreSQL | Documentos de Microsoft"'
description: 'Ejemplo de script de la CLI de Azure: crea un servidor de Azure Database for PostgreSQL (Base de datos de Azure para PostgreSQL) y configura una regla de firewall de nivel de servidor.'
services: postgresql
author: salonisonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: azure-cli
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: bbe31f77283aa4a3bb36d1fd9171c280594a8267
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-postgresql-server-and-configure-a-firewall-rule-using-hello-azure-cli"></a><span data-ttu-id="c0b88-103">Crear una base de datos de Azure para servidor de PostgreSQL y configurar una regla de firewall mediante Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="c0b88-103">Create an Azure Database for PostgreSQL server and configure a firewall rule using hello Azure CLI</span></span>
<span data-ttu-id="c0b88-104">Este script de la CLI de ejemplo crea un servidor de Azure Database for PostgreSQL (Base de datos de Azure para PostgreSQL) y configura una regla de firewall de nivel de servidor.</span><span class="sxs-lookup"><span data-stu-id="c0b88-104">This sample CLI script creates an Azure Database for PostgreSQL server and configures a server-level firewall rule.</span></span> <span data-ttu-id="c0b88-105">Una vez que se ha ejecutado correctamente el script de Hola, servidor de PostgreSQL Hola puede tener acceso desde todos los servicios de Azure y Hola configurado direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="c0b88-105">Once hello script has been successfully run, hello PostgreSQL server can be accessed from all Azure services and hello configured IP address.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c0b88-106">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="c0b88-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="c0b88-107">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0b88-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="c0b88-108">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c0b88-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="c0b88-109">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="c0b88-109">Sample script</span></span>
<span data-ttu-id="c0b88-110">En este script de ejemplo, editar Hola resaltada las líneas toocustomize Hola administrador username y password.</span><span class="sxs-lookup"><span data-stu-id="c0b88-110">In this sample script, edit hello highlighted lines toocustomize hello admin username and password.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/create-postgresql-server-and-firewall-rule.sh?highlight=15-16 "Create an Azure Database for PostgreSQL, and server-level firewall rule.")]

## <a name="clean-up-deployment"></a><span data-ttu-id="c0b88-111">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="c0b88-111">Clean up deployment</span></span>
<span data-ttu-id="c0b88-112">Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser usado tooremove grupo de recursos de Hola y todos los recursos asociados con él.</span><span class="sxs-lookup"><span data-stu-id="c0b88-112">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/delete-postgresql.sh "Delete hello resource group.")]

## <a name="script-explanation"></a><span data-ttu-id="c0b88-113">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="c0b88-113">Script explanation</span></span>
<span data-ttu-id="c0b88-114">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="c0b88-114">This script uses hello following commands.</span></span> <span data-ttu-id="c0b88-115">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="c0b88-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c0b88-116">**Comando**</span><span class="sxs-lookup"><span data-stu-id="c0b88-116">**Command**</span></span> | <span data-ttu-id="c0b88-117">**Notas**</span><span class="sxs-lookup"><span data-stu-id="c0b88-117">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="c0b88-118">az group create</span><span class="sxs-lookup"><span data-stu-id="c0b88-118">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="c0b88-119">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="c0b88-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c0b88-120">az postgres server create</span><span class="sxs-lookup"><span data-stu-id="c0b88-120">az postgres server create</span></span>](/cli/azure/postgres/server#create) | <span data-ttu-id="c0b88-121">Crea un servidor de PostgreSQL que hospeda las bases de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0b88-121">Creates a PostgreSQL server that hosts hello databases.</span></span> |
| [<span data-ttu-id="c0b88-122">az postgres server firewall create</span><span class="sxs-lookup"><span data-stu-id="c0b88-122">az postgres server firewall create</span></span>](/cli/azure/postgres/server/firewall-rule#create) | <span data-ttu-id="c0b88-123">Crea un servidor de toohello de acceso de firewall regla tooallow y bases de datos en él desde el intervalo de direcciones IP de hello especificado.</span><span class="sxs-lookup"><span data-stu-id="c0b88-123">Creates a firewall rule tooallow access toohello server and databases under it from hello entered IP address range.</span></span> |
| [<span data-ttu-id="c0b88-124">az group delete</span><span class="sxs-lookup"><span data-stu-id="c0b88-124">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="c0b88-125">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="c0b88-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c0b88-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c0b88-126">Next steps</span></span>
- <span data-ttu-id="c0b88-127">Obtener información detallada sobre Hola CLI de Azure: [documentación de CLI de Azure](/cli/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="c0b88-127">Read more information on hello Azure CLI: [Azure CLI documentation](/cli/azure/overview)</span></span>
- <span data-ttu-id="c0b88-128">Pruebe otros scripts adicionales: [Ejemplos de la CLI de Azure para Azure Database for PostgreSQL](../sample-scripts-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c0b88-128">Try additional scripts: [Azure CLI samples for Azure Database for PostgreSQL](../sample-scripts-azure-cli.md)</span></span>
