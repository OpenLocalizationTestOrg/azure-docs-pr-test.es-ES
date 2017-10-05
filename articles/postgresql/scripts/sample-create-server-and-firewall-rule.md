---
title: "Script de la CLI de Azure: creación de Azure Database for PostgreSQL (Base de datos de Azure para PostgreSQL) | Microsoft Docs"
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
ms.openlocfilehash: e545b568cd57fdcf28ab33a5ebfa34a495111c7f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-azure-database-for-postgresql-server-and-configure-a-firewall-rule-using-the-azure-cli"></a><span data-ttu-id="c1d04-103">Creación de una base de datos de Azure para el servidor PostgreSQL y configuración de una regla de firewall mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="c1d04-103">Create an Azure Database for PostgreSQL server and configure a firewall rule using the Azure CLI</span></span>
<span data-ttu-id="c1d04-104">Este script de la CLI de ejemplo crea un servidor de Azure Database for PostgreSQL (Base de datos de Azure para PostgreSQL) y configura una regla de firewall de nivel de servidor.</span><span class="sxs-lookup"><span data-stu-id="c1d04-104">This sample CLI script creates an Azure Database for PostgreSQL server and configures a server-level firewall rule.</span></span> <span data-ttu-id="c1d04-105">Después de ejecutar el script correctamente, el servidor PostgreSQL es accesible desde todos los servicios de Azure y la dirección IP configurada.</span><span class="sxs-lookup"><span data-stu-id="c1d04-105">Once the script has been successfully run, the PostgreSQL server can be accessed from all Azure services and the configured IP address.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c1d04-106">Si decide instalar y usar la CLI localmente, para este tema es preciso que ejecute la CLI de Azure versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="c1d04-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="c1d04-107">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="c1d04-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="c1d04-108">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c1d04-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="c1d04-109">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="c1d04-109">Sample script</span></span>
<span data-ttu-id="c1d04-110">En este script de ejemplo, edite las líneas resaltadas para personalizar el nombre de usuario y la contraseña de administrador.</span><span class="sxs-lookup"><span data-stu-id="c1d04-110">In this sample script, edit the highlighted lines to customize the admin username and password.</span></span>
<span data-ttu-id="c1d04-111">[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/create-postgresql-server-and-firewall-rule.sh?highlight=15-16 "Cree una instancia de Azure Database for PostgreSQL y una regla de firewall de nivel de servidor.")]</span><span class="sxs-lookup"><span data-stu-id="c1d04-111">[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/create-postgresql-server-and-firewall-rule.sh?highlight=15-16 "Create an Azure Database for PostgreSQL, and server-level firewall rule.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="c1d04-112">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="c1d04-112">Clean up deployment</span></span>
<span data-ttu-id="c1d04-113">Después de ejecutar el script de ejemplo, se puede usar el comando siguiente para quitar el grupo de recursos y todos los recursos asociados.</span><span class="sxs-lookup"><span data-stu-id="c1d04-113">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>
<span data-ttu-id="c1d04-114">[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/delete-postgresql.sh "Elimine el grupo de recursos.")]</span><span class="sxs-lookup"><span data-stu-id="c1d04-114">[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/delete-postgresql.sh "Delete the resource group.")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="c1d04-115">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="c1d04-115">Script explanation</span></span>
<span data-ttu-id="c1d04-116">Este script usa los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="c1d04-116">This script uses the following commands.</span></span> <span data-ttu-id="c1d04-117">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="c1d04-117">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c1d04-118">**Comando**</span><span class="sxs-lookup"><span data-stu-id="c1d04-118">**Command**</span></span> | <span data-ttu-id="c1d04-119">**Notas**</span><span class="sxs-lookup"><span data-stu-id="c1d04-119">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="c1d04-120">az group create</span><span class="sxs-lookup"><span data-stu-id="c1d04-120">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="c1d04-121">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="c1d04-121">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c1d04-122">az postgres server create</span><span class="sxs-lookup"><span data-stu-id="c1d04-122">az postgres server create</span></span>](/cli/azure/postgres/server#create) | <span data-ttu-id="c1d04-123">Crea un servidor de PostgreSQL que hospeda las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="c1d04-123">Creates a PostgreSQL server that hosts the databases.</span></span> |
| [<span data-ttu-id="c1d04-124">az postgres server firewall create</span><span class="sxs-lookup"><span data-stu-id="c1d04-124">az postgres server firewall create</span></span>](/cli/azure/postgres/server/firewall-rule#create) | <span data-ttu-id="c1d04-125">Crea una regla de firewall para permitir el acceso al servidor y las bases de datos de este desde el intervalo de direcciones IP especificado.</span><span class="sxs-lookup"><span data-stu-id="c1d04-125">Creates a firewall rule to allow access to the server and databases under it from the entered IP address range.</span></span> |
| [<span data-ttu-id="c1d04-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="c1d04-126">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="c1d04-127">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="c1d04-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c1d04-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c1d04-128">Next steps</span></span>
- <span data-ttu-id="c1d04-129">Para más información sobre la CLI de Azure, vea la [documentación de la CLI de Azure](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c1d04-129">Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure/overview)</span></span>
- <span data-ttu-id="c1d04-130">Pruebe otros scripts adicionales: [Ejemplos de la CLI de Azure para Azure Database for PostgreSQL](../sample-scripts-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c1d04-130">Try additional scripts: [Azure CLI samples for Azure Database for PostgreSQL](../sample-scripts-azure-cli.md)</span></span>
