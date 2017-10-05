---
title: 'Script de la CLI de Azure: escalado de Azure Database for PostgreSQL (Base de datos de Azure para PostgreSQL) | Microsoft Docs'
description: "Ejemplo de script de la CLI de Azure: escalado del servidor de Azure Database for PostgreSQL (Base de datos de Azure para PostgreSQL) a un nivel de rendimiento diferente después de consultar las métricas."
services: postgresql
author: salonisonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.custom: mvc
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: b847abb336cce5dd5516469dca58002d3ba265f0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="monitor-and-scale-a-single-postgresql-server-using-azure-cli"></a><span data-ttu-id="86bcd-103">Supervisión y escalado de un solo servidor PostgreSQL mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="86bcd-103">Monitor and scale a single PostgreSQL server using Azure CLI</span></span>
<span data-ttu-id="86bcd-104">Este script de la CLI de ejemplo escala un solo servidor de Azure Database for PostgreSQL (Base de datos de Azure para PostgreSQL) a un nivel de rendimiento diferente después de consultar las métricas.</span><span class="sxs-lookup"><span data-stu-id="86bcd-104">This sample CLI script scales a single Azure Database for PostgreSQL server to a different performance level after querying the metrics.</span></span> 

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="86bcd-105">Si decide instalar y usar la CLI localmente, para este tema es preciso que ejecute la CLI de Azure versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="86bcd-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="86bcd-106">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="86bcd-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="86bcd-107">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="86bcd-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="86bcd-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="86bcd-108">Sample script</span></span>
<span data-ttu-id="86bcd-109">En este script de ejemplo, cambie las líneas resaltadas para personalizar el nombre de usuario de administrador y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="86bcd-109">In this sample script, change the highlighted lines to customize the admin username and password.</span></span> <span data-ttu-id="86bcd-110">Reemplace el identificador de suscripción usado en los comandos de monitor az por su propio identificador de suscripción. [!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/scale-postgresql-server.sh?highlight=15-16 "Cree y escale una instancia de Azure Database for PostgreSQL (Base de datos de Azure para PostgreSQL).")]</span><span class="sxs-lookup"><span data-stu-id="86bcd-110">Replace the subscription id used in the az monitor commands with your own subscription id. [!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/scale-postgresql-server.sh?highlight=15-16 "Create and scale Azure Database for PostgreSQL.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="86bcd-111">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="86bcd-111">Clean up deployment</span></span>
<span data-ttu-id="86bcd-112">Después de ejecutar el script de ejemplo, se puede usar el comando siguiente para quitar el grupo de recursos y todos los recursos asociados.</span><span class="sxs-lookup"><span data-stu-id="86bcd-112">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>
<span data-ttu-id="86bcd-113">[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/delete-postgresql.sh "Elimine el grupo de recursos.")]</span><span class="sxs-lookup"><span data-stu-id="86bcd-113">[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/delete-postgresql.sh "Delete the resource group.")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="86bcd-114">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="86bcd-114">Script explanation</span></span>
<span data-ttu-id="86bcd-115">Este script usa los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="86bcd-115">This script uses the following commands.</span></span> <span data-ttu-id="86bcd-116">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="86bcd-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="86bcd-117">**Comando**</span><span class="sxs-lookup"><span data-stu-id="86bcd-117">**Command**</span></span> | <span data-ttu-id="86bcd-118">**Notas**</span><span class="sxs-lookup"><span data-stu-id="86bcd-118">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="86bcd-119">az group create</span><span class="sxs-lookup"><span data-stu-id="86bcd-119">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="86bcd-120">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="86bcd-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="86bcd-121">az postgres server create</span><span class="sxs-lookup"><span data-stu-id="86bcd-121">az postgres server create</span></span>](/cli/azure/postgres/server#create) | <span data-ttu-id="86bcd-122">Crea un servidor PostgreSQL que hospeda las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="86bcd-122">Creates a PostgreSQL server that hosts the databases.</span></span> |
| [<span data-ttu-id="86bcd-123">az monitor metrics list</span><span class="sxs-lookup"><span data-stu-id="86bcd-123">az monitor metrics list</span></span>](/cli/azure/monitor/metrics#list) | <span data-ttu-id="86bcd-124">Especifica el valor de métrica de los recursos.</span><span class="sxs-lookup"><span data-stu-id="86bcd-124">List the metric value for the resources.</span></span> |
| [<span data-ttu-id="86bcd-125">az group delete</span><span class="sxs-lookup"><span data-stu-id="86bcd-125">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="86bcd-126">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="86bcd-126">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="86bcd-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="86bcd-127">Next steps</span></span>
- <span data-ttu-id="86bcd-128">Para más información sobre la CLI de Azure, vea la [documentación de la CLI de Azure](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="86bcd-128">Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure/overview)</span></span>
- <span data-ttu-id="86bcd-129">Pruebe otros scripts adicionales: [Ejemplos de la CLI de Azure para Azure Database for PostgreSQL](../sample-scripts-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="86bcd-129">Try additional scripts: [Azure CLI samples for Azure Database for PostgreSQL](../sample-scripts-azure-cli.md)</span></span>
- <span data-ttu-id="86bcd-130">Para más información sobre el escalado, vea [Niveles de servicio](../concepts-service-tiers.md) y [Unidades de proceso y almacenamiento](../concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="86bcd-130">Read more information on scaling: [Service Tiers](../concepts-service-tiers.md) and [Compute Units and Storage Units](../concepts-compute-unit-and-storage.md)</span></span>
