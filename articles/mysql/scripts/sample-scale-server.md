---
title: Ejemplos de la CLI de Azure para escalar un servidor de Azure Database for MySQL | Microsoft Docs
description: "Este script de la CLI de ejemplo escala el servidor de Azure Database for MySQL (Base de datos de Azure para MySQL) a un nivel de rendimiento diferente después de consultar las métricas."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: sample
ms.custom: mvc
ms.date: 05/31/2017
ms.openlocfilehash: 33316ff3db382d25a444d55772c6ee4d7b7ac418
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-scale-an-azure-database-for-mysql-server-using-azure-cli"></a><span data-ttu-id="35e89-103">Supervisión y escalado de un servidor de Azure Database for MySQL (Base de datos de Azure para MySQL) mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="35e89-103">Monitor and scale an Azure Database for MySQL server using Azure CLI</span></span>
<span data-ttu-id="35e89-104">Este script de la CLI de ejemplo escala un solo servidor de Azure Database for MySQL (Base de datos de Azure para MySQL) a un nivel de rendimiento diferente después de consultar las métricas.</span><span class="sxs-lookup"><span data-stu-id="35e89-104">This sample CLI script scales a single Azure Database for MySQL server to a different performance level after querying the metrics.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="35e89-105">Si decide instalar y usar la CLI localmente, para este tema es preciso que ejecute la CLI de Azure versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="35e89-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="35e89-106">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="35e89-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="35e89-107">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="35e89-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="35e89-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="35e89-108">Sample script</span></span>
<span data-ttu-id="35e89-109">En este script de ejemplo, cambie las líneas resaltadas para personalizar el nombre de usuario de administrador y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="35e89-109">In this sample script, change the highlighted lines to customize the admin username and password.</span></span> <span data-ttu-id="35e89-110">Reemplace el identificador de suscripción usado en los comandos de monitor az por su propio identificador de suscripción.</span><span class="sxs-lookup"><span data-stu-id="35e89-110">Replace the subscription id used in the az monitor commands with your own subscription id.</span></span>
<span data-ttu-id="35e89-111">[!code-azurecli-interactive[principal](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=15-16 "Cree y escale una base de datos de Azure para MySQL.")]</span><span class="sxs-lookup"><span data-stu-id="35e89-111">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=15-16 "Create and scale Azure Database for MySQL.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="35e89-112">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="35e89-112">Clean up deployment</span></span>
<span data-ttu-id="35e89-113">Después de ejecutar el script de ejemplo, se puede usar el comando siguiente para quitar el grupo de recursos y todos los recursos asociados.</span><span class="sxs-lookup"><span data-stu-id="35e89-113">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>
<span data-ttu-id="35e89-114">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/delete-mysql.sh  "Elimine el grupo de recursos.")]</span><span class="sxs-lookup"><span data-stu-id="35e89-114">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/delete-mysql.sh  "Delete the resource group.")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="35e89-115">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="35e89-115">Script explanation</span></span>
<span data-ttu-id="35e89-116">Este script usa los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="35e89-116">This script uses the following commands.</span></span> <span data-ttu-id="35e89-117">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="35e89-117">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="35e89-118">**Comando**</span><span class="sxs-lookup"><span data-stu-id="35e89-118">**Command**</span></span> | <span data-ttu-id="35e89-119">**Notas**</span><span class="sxs-lookup"><span data-stu-id="35e89-119">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="35e89-120">az group create</span><span class="sxs-lookup"><span data-stu-id="35e89-120">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="35e89-121">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="35e89-121">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="35e89-122">az mysql server create</span><span class="sxs-lookup"><span data-stu-id="35e89-122">az mysql server create</span></span>](/cli/azure/mysql/server#create) | <span data-ttu-id="35e89-123">Crea un servidor MySQL que hospeda las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="35e89-123">Creates a MySQL server that hosts the databases.</span></span> |
| [<span data-ttu-id="35e89-124">az monitor metrics list</span><span class="sxs-lookup"><span data-stu-id="35e89-124">az monitor metrics list</span></span>](/cli/azure/monitor/metrics#list) | <span data-ttu-id="35e89-125">Especifica el valor de métrica de los recursos.</span><span class="sxs-lookup"><span data-stu-id="35e89-125">List the metric value for the resources.</span></span> |
| [<span data-ttu-id="35e89-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="35e89-126">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="35e89-127">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="35e89-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="35e89-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="35e89-128">Next steps</span></span>
- <span data-ttu-id="35e89-129">Para más información sobre la CLI de Azure: [Documentación de la CLI de Azure](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="35e89-129">Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure/overview).</span></span>
- <span data-ttu-id="35e89-130">Pruebe scripts adicionales en [Ejemplos de la CLI de Azure para la base de datos de Azure para MySQL](../sample-scripts-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="35e89-130">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span></span>
- <span data-ttu-id="35e89-131">Para obtener más información sobre el escalado, consulte [Service Tiers](../concepts-service-tiers.md) (Niveles de servicio) y [Compute Units and Storage Units](../concepts-compute-unit-and-storage.md) (Unidades de proceso y almacenamiento).</span><span class="sxs-lookup"><span data-stu-id="35e89-131">For more information on scaling, see [Service Tiers](../concepts-service-tiers.md) and [Compute Units and Storage Units](../concepts-compute-unit-and-storage.md).</span></span>
