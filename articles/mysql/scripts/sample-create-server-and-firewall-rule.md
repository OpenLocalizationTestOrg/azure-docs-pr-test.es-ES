---
title: 'Script de la CLI de Azure: crear una base de datos de Azure Database for MySQL | Microsoft Docs'
description: Este script de la CLI de ejemplo crea un servidor de Azure Database for MySQL (Base de datos de Azure para MySQL) y configura una regla de firewall de nivel de servidor.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.custom: mvc
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: 201db294ce362ef3e09cbe62f48bd51c8ea94dbb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-mysql-server-and-configure-a-firewall-rule-using-the-azure-cli"></a><span data-ttu-id="6bc21-103">Cree un servidor MySQL y configure una regla de firewall mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="6bc21-103">Create a MySQL server and configure a firewall rule using the Azure CLI</span></span>
<span data-ttu-id="6bc21-104">Este script de la CLI de ejemplo crea un servidor de Azure Database for MySQL (Base de datos de Azure para MySQL) y configura una regla de firewall de nivel de servidor.</span><span class="sxs-lookup"><span data-stu-id="6bc21-104">This sample CLI script creates an Azure Database for MySQL server and configures a server-level firewall rule.</span></span> <span data-ttu-id="6bc21-105">Una vez que el script se ejecuta correctamente, todos los servicios de Azure y la dirección IP configurada pueden tener acceso al servidor MySQL.</span><span class="sxs-lookup"><span data-stu-id="6bc21-105">Once the script runs successfully, the MySQL server is accessible by all Azure services and the configured IP address.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6bc21-106">Si decide instalar y usar la CLI localmente, para este tema es preciso que ejecute la CLI de Azure versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="6bc21-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="6bc21-107">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="6bc21-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="6bc21-108">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6bc21-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="6bc21-109">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="6bc21-109">Sample script</span></span>
<span data-ttu-id="6bc21-110">En este script de ejemplo, edite las líneas resaltadas para personalizar el nombre de usuario y la contraseña de administrador.</span><span class="sxs-lookup"><span data-stu-id="6bc21-110">In this sample script, edit the highlighted lines to customize the admin username and password.</span></span>
<span data-ttu-id="6bc21-111">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/create-mysql-server-and-firewall-rule.sh?highlight=15-16 "Cree una instancia de Azure Database for MySQL y una regla de firewall de nivel de servidor.")]</span><span class="sxs-lookup"><span data-stu-id="6bc21-111">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/create-mysql-server-and-firewall-rule.sh?highlight=15-16 "Create an Azure Database for MySQL, and server-level firewall rule.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="6bc21-112">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="6bc21-112">Clean up deployment</span></span>
<span data-ttu-id="6bc21-113">Después de ejecutar el script de ejemplo, se puede usar el comando siguiente para quitar el grupo de recursos y todos los recursos asociados.</span><span class="sxs-lookup"><span data-stu-id="6bc21-113">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>
<span data-ttu-id="6bc21-114">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/delete-mysql.sh "Elimine el grupo de recursos.")]</span><span class="sxs-lookup"><span data-stu-id="6bc21-114">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/delete-mysql.sh "Delete the resource group.")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="6bc21-115">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="6bc21-115">Script explanation</span></span>
<span data-ttu-id="6bc21-116">Este script usa los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="6bc21-116">This script uses the following commands.</span></span> <span data-ttu-id="6bc21-117">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="6bc21-117">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6bc21-118">**Comando**</span><span class="sxs-lookup"><span data-stu-id="6bc21-118">**Command**</span></span> | <span data-ttu-id="6bc21-119">**Notas**</span><span class="sxs-lookup"><span data-stu-id="6bc21-119">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="6bc21-120">az group create</span><span class="sxs-lookup"><span data-stu-id="6bc21-120">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="6bc21-121">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="6bc21-121">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6bc21-122">az mysql server create</span><span class="sxs-lookup"><span data-stu-id="6bc21-122">az mysql server create</span></span>](/cli/azure/mysql/server#create) | <span data-ttu-id="6bc21-123">Crea un servidor MySQL que hospeda las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="6bc21-123">Creates a MySQL server that hosts the databases.</span></span> |
| [<span data-ttu-id="6bc21-124">az mysql server firewall create</span><span class="sxs-lookup"><span data-stu-id="6bc21-124">az mysql server firewall create</span></span>](/cli/azure/mysql/server/firewall-rule#create) | <span data-ttu-id="6bc21-125">Crea una regla de firewall para permitir el acceso al servidor y las bases de datos de este desde el intervalo de direcciones IP especificado.</span><span class="sxs-lookup"><span data-stu-id="6bc21-125">Creates a firewall rule to allow access to the server and databases under it from the entered IP address range.</span></span> |
| [<span data-ttu-id="6bc21-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="6bc21-126">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="6bc21-127">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="6bc21-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6bc21-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6bc21-128">Next steps</span></span>
- <span data-ttu-id="6bc21-129">Para más información sobre la CLI de Azure: [Documentación de la CLI de Azure](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6bc21-129">Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure/overview).</span></span>
- <span data-ttu-id="6bc21-130">Pruebe scripts adicionales en: [Ejemplos de la CLI de Azure para Azure Database for MySQL](../sample-scripts-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="6bc21-130">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span></span>
