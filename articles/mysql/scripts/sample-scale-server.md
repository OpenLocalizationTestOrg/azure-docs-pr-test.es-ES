---
title: ejemplos de aaaAzure CLI tooscale una base de datos de MySQL server | Documentos de Microsoft
description: "Esta secuencia de comandos CLI de ejemplo escala base de datos de Azure para el nivel de rendimiento de MySQL server tooa después de consultar las métricas de Hola."
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
ms.openlocfilehash: 721ef9db35a5f3be7a38438c1abb724187b18b75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-scale-an-azure-database-for-mysql-server-using-azure-cli"></a><span data-ttu-id="9c6ce-103">Supervisión y escalado de un servidor de Azure Database for MySQL (Base de datos de Azure para MySQL) mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="9c6ce-103">Monitor and scale an Azure Database for MySQL server using Azure CLI</span></span>
<span data-ttu-id="9c6ce-104">Esta secuencia de comandos CLI de ejemplo, amplía una sola base de datos de Azure para el nivel de rendimiento de MySQL server tooa después de consultar las métricas de Hola.</span><span class="sxs-lookup"><span data-stu-id="9c6ce-104">This sample CLI script scales a single Azure Database for MySQL server tooa different performance level after querying hello metrics.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9c6ce-105">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="9c6ce-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="9c6ce-106">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="9c6ce-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="9c6ce-107">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9c6ce-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="9c6ce-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="9c6ce-108">Sample script</span></span>
<span data-ttu-id="9c6ce-109">En este script de ejemplo, cambie Hola resaltada las líneas toocustomize Hola administrador username y password.</span><span class="sxs-lookup"><span data-stu-id="9c6ce-109">In this sample script, change hello highlighted lines toocustomize hello admin username and password.</span></span> <span data-ttu-id="9c6ce-110">Reemplace el Id. de suscripción de hello utilizado en comandos de monitor de hello az con su propio identificador de suscripción.[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=15-16 "Create and scale Azure Database for MySQL.")]</span><span class="sxs-lookup"><span data-stu-id="9c6ce-110">Replace hello subscription id used in hello az monitor commands with your own subscription id. [!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=15-16 "Create and scale Azure Database for MySQL.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="9c6ce-111">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="9c6ce-111">Clean up deployment</span></span>
<span data-ttu-id="9c6ce-112">Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser usado tooremove grupo de recursos de Hola y todos los recursos asociados con él.</span><span class="sxs-lookup"><span data-stu-id="9c6ce-112">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/delete-mysql.sh  "Delete hello resource group.")]

## <a name="script-explanation"></a><span data-ttu-id="9c6ce-113">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="9c6ce-113">Script explanation</span></span>
<span data-ttu-id="9c6ce-114">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="9c6ce-114">This script uses hello following commands.</span></span> <span data-ttu-id="9c6ce-115">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="9c6ce-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="9c6ce-116">**Comando**</span><span class="sxs-lookup"><span data-stu-id="9c6ce-116">**Command**</span></span> | <span data-ttu-id="9c6ce-117">**Notas**</span><span class="sxs-lookup"><span data-stu-id="9c6ce-117">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="9c6ce-118">az group create</span><span class="sxs-lookup"><span data-stu-id="9c6ce-118">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="9c6ce-119">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="9c6ce-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9c6ce-120">az mysql server create</span><span class="sxs-lookup"><span data-stu-id="9c6ce-120">az mysql server create</span></span>](/cli/azure/mysql/server#create) | <span data-ttu-id="9c6ce-121">Crea un servidor de MySQL que hospeda las bases de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="9c6ce-121">Creates a MySQL server that hosts hello databases.</span></span> |
| [<span data-ttu-id="9c6ce-122">az monitor metrics list</span><span class="sxs-lookup"><span data-stu-id="9c6ce-122">az monitor metrics list</span></span>](/cli/azure/monitor/metrics#list) | <span data-ttu-id="9c6ce-123">Valor de métrica de Hola de lista de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="9c6ce-123">List hello metric value for hello resources.</span></span> |
| [<span data-ttu-id="9c6ce-124">az group delete</span><span class="sxs-lookup"><span data-stu-id="9c6ce-124">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="9c6ce-125">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="9c6ce-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9c6ce-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9c6ce-126">Next steps</span></span>
- <span data-ttu-id="9c6ce-127">Obtener información detallada sobre Hola CLI de Azure: [documentación de Azure CLI](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9c6ce-127">Read more information on hello Azure CLI: [Azure CLI documentation](/cli/azure/overview).</span></span>
- <span data-ttu-id="9c6ce-128">Pruebe scripts adicionales en: [Ejemplos de la CLI de Azure para Azure Database for MySQL](../sample-scripts-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="9c6ce-128">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span></span>
- <span data-ttu-id="9c6ce-129">Para obtener más información sobre el escalado, consulte [Service Tiers](../concepts-service-tiers.md) (Niveles de servicio) y [Compute Units and Storage Units](../concepts-compute-unit-and-storage.md) (Unidades de proceso y almacenamiento).</span><span class="sxs-lookup"><span data-stu-id="9c6ce-129">For more information on scaling, see [Service Tiers](../concepts-service-tiers.md) and [Compute Units and Storage Units](../concepts-compute-unit-and-storage.md).</span></span>
