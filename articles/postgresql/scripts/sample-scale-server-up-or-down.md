---
title: aaa "base de datos de Azure de la escala de la secuencia de comandos CLI de Azure para PostgreSQL | Documentos de Microsoft"
description: "Ejemplo de secuencia de comandos para Azure CLI - base de datos de Azure de escala de nivel de rendimiento diferentes de PostgreSQL servidor tooa después de consultar las métricas de Hola."
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
ms.openlocfilehash: 678b28941dbb4334cb374d4888991a00b44966b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-scale-a-single-postgresql-server-using-azure-cli"></a><span data-ttu-id="0db5e-103">Supervisión y escalado de un solo servidor PostgreSQL mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="0db5e-103">Monitor and scale a single PostgreSQL server using Azure CLI</span></span>
<span data-ttu-id="0db5e-104">Esta secuencia de comandos CLI de ejemplo, amplía una sola base de datos de Azure para el nivel de rendimiento diferentes de PostgreSQL servidor tooa después de consultar las métricas de Hola.</span><span class="sxs-lookup"><span data-stu-id="0db5e-104">This sample CLI script scales a single Azure Database for PostgreSQL server tooa different performance level after querying hello metrics.</span></span> 

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="0db5e-105">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="0db5e-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="0db5e-106">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="0db5e-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="0db5e-107">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0db5e-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="0db5e-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="0db5e-108">Sample script</span></span>
<span data-ttu-id="0db5e-109">En este script de ejemplo, cambie Hola resaltada las líneas toocustomize Hola administrador username y password.</span><span class="sxs-lookup"><span data-stu-id="0db5e-109">In this sample script, change hello highlighted lines toocustomize hello admin username and password.</span></span> <span data-ttu-id="0db5e-110">Reemplace el Id. de suscripción de hello utilizado en comandos de monitor de hello az con su propio identificador de suscripción.[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/scale-postgresql-server.sh?highlight=15-16 "Create and scale Azure Database for PostgreSQL.")]</span><span class="sxs-lookup"><span data-stu-id="0db5e-110">Replace hello subscription id used in hello az monitor commands with your own subscription id. [!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/scale-postgresql-server.sh?highlight=15-16 "Create and scale Azure Database for PostgreSQL.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="0db5e-111">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="0db5e-111">Clean up deployment</span></span>
<span data-ttu-id="0db5e-112">Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser usado tooremove grupo de recursos de Hola y todos los recursos asociados con él.</span><span class="sxs-lookup"><span data-stu-id="0db5e-112">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/delete-postgresql.sh "Delete hello resource group.")]

## <a name="script-explanation"></a><span data-ttu-id="0db5e-113">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="0db5e-113">Script explanation</span></span>
<span data-ttu-id="0db5e-114">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="0db5e-114">This script uses hello following commands.</span></span> <span data-ttu-id="0db5e-115">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="0db5e-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="0db5e-116">**Comando**</span><span class="sxs-lookup"><span data-stu-id="0db5e-116">**Command**</span></span> | <span data-ttu-id="0db5e-117">**Notas**</span><span class="sxs-lookup"><span data-stu-id="0db5e-117">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="0db5e-118">az group create</span><span class="sxs-lookup"><span data-stu-id="0db5e-118">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="0db5e-119">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="0db5e-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0db5e-120">az postgres server create</span><span class="sxs-lookup"><span data-stu-id="0db5e-120">az postgres server create</span></span>](/cli/azure/postgres/server#create) | <span data-ttu-id="0db5e-121">Crea un servidor de PostgreSQL que hospeda las bases de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="0db5e-121">Creates a PostgreSQL server that hosts hello databases.</span></span> |
| [<span data-ttu-id="0db5e-122">az monitor metrics list</span><span class="sxs-lookup"><span data-stu-id="0db5e-122">az monitor metrics list</span></span>](/cli/azure/monitor/metrics#list) | <span data-ttu-id="0db5e-123">Valor de métrica de Hola de lista de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="0db5e-123">List hello metric value for hello resources.</span></span> |
| [<span data-ttu-id="0db5e-124">az group delete</span><span class="sxs-lookup"><span data-stu-id="0db5e-124">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="0db5e-125">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="0db5e-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0db5e-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0db5e-126">Next steps</span></span>
- <span data-ttu-id="0db5e-127">Obtener información detallada sobre Hola CLI de Azure: [documentación de CLI de Azure](/cli/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="0db5e-127">Read more information on hello Azure CLI: [Azure CLI documentation](/cli/azure/overview)</span></span>
- <span data-ttu-id="0db5e-128">Pruebe otros scripts adicionales: [Ejemplos de la CLI de Azure para Azure Database for PostgreSQL](../sample-scripts-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="0db5e-128">Try additional scripts: [Azure CLI samples for Azure Database for PostgreSQL](../sample-scripts-azure-cli.md)</span></span>
- <span data-ttu-id="0db5e-129">Para más información sobre el escalado, vea [Niveles de servicio](../concepts-service-tiers.md) y [Unidades de proceso y almacenamiento](../concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="0db5e-129">Read more information on scaling: [Service Tiers](../concepts-service-tiers.md) and [Compute Units and Storage Units](../concepts-compute-unit-and-storage.md)</span></span>
