---
title: aaaAzure ejemplo de secuencia de comandos de CLI - ejecutando un trabajo con lote | Documentos de Microsoft
description: "Ejemplo de script de la CLI de Azure - Ejecución de un trabajo con Batch"
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: f73a7cb341e550fd1c92f92201e20b27fa20d238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="running-jobs-on-azure-batch-with-azure-cli"></a><span data-ttu-id="ec966-103">Ejecución de trabajos en Azure Batch con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="ec966-103">Running jobs on Azure Batch with Azure CLI</span></span>

<span data-ttu-id="ec966-104">Este script crea un trabajo por lotes y agrega una serie de trabajo de toohello de tareas.</span><span class="sxs-lookup"><span data-stu-id="ec966-104">This script creates a Batch job and adds a series of tasks toohello job.</span></span> <span data-ttu-id="ec966-105">También se muestra cómo toomonitor un trabajo y sus tareas.</span><span class="sxs-lookup"><span data-stu-id="ec966-105">It also demonstrates how toomonitor a job and its tasks.</span></span> <span data-ttu-id="ec966-106">Por último, se muestra cómo tooquery Hola servicio por lotes eficaz para obtener información acerca de las tareas del trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ec966-106">Finally, it shows how tooquery hello Batch service efficiently for information about hello job's tasks.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ec966-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ec966-107">Prerequisites</span></span>

- <span data-ttu-id="ec966-108">Instalación Hola CLI de Azure utilizando instrucciones de hello proporcionadas en hello [Guía de instalación de CLI de Azure](https://docs.microsoft.com/cli/azure/install-azure-cli), si aún no lo ha hecho.</span><span class="sxs-lookup"><span data-stu-id="ec966-108">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="ec966-109">Cree una cuenta de Batch si aún no tiene una.</span><span class="sxs-lookup"><span data-stu-id="ec966-109">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="ec966-110">Vea [crear una cuenta de lote con hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) para una secuencia de comandos de ejemplo que crea una cuenta.</span><span class="sxs-lookup"><span data-stu-id="ec966-110">See [Create a Batch account with hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>
- <span data-ttu-id="ec966-111">Configurar una toorun de aplicación de una tarea de inicio si aún no lo ha hecho.</span><span class="sxs-lookup"><span data-stu-id="ec966-111">Configure an application toorun from a start task if you haven't yet done so.</span></span> <span data-ttu-id="ec966-112">Vea [agregar aplicaciones tooAzure por lotes con Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) para una secuencia de comandos de ejemplo que crea una aplicación y carga un tooAzure del paquete de aplicación.</span><span class="sxs-lookup"><span data-stu-id="ec966-112">See [Adding applications tooAzure Batch with Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) for a sample script that creates an application and uploads an application package tooAzure.</span></span>
- <span data-ttu-id="ec966-113">Configurar un grupo de en qué Hola se ejecutará el trabajo.</span><span class="sxs-lookup"><span data-stu-id="ec966-113">Configure a pool on which hello job will run.</span></span> <span data-ttu-id="ec966-114">Consulte [Administración de grupos de Azure Batch con la CLI de Azure](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool) para ver un script de ejemplo que crea un grupo con una configuración de servicios en la nube o de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="ec966-114">See [Managing Azure Batch pools with Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool) for a sample script that creates a pool with either a Cloud Service Configuration or a Virtual Machine Configuration.</span></span>

## <a name="sample-script"></a><span data-ttu-id="ec966-115">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="ec966-115">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/run-job/run-job.sh "Run Job")]

## <a name="clean-up-job"></a><span data-ttu-id="ec966-116">Limpieza de un trabajo</span><span class="sxs-lookup"><span data-stu-id="ec966-116">Clean up job</span></span>

<span data-ttu-id="ec966-117">Después de ejecutar Hola por encima de la secuencia de comandos de ejemplo, ejecute hello después comando tooremove el trabajo y todas sus tareas.</span><span class="sxs-lookup"><span data-stu-id="ec966-117">After you run hello above sample script, run hello following command tooremove the job and all of its tasks.</span></span> <span data-ttu-id="ec966-118">Tenga en cuenta que el grupo de hello necesitará toobe eliminar por separado.</span><span class="sxs-lookup"><span data-stu-id="ec966-118">Note that hello pool will need toobe deleted separately.</span></span> <span data-ttu-id="ec966-119">Consulte [Administración de grupos de Azure Batch con la CLI de Azure](./batch-cli-sample-manage-pool.md) para obtener más información sobre cómo crear y eliminar grupos.</span><span class="sxs-lookup"><span data-stu-id="ec966-119">See [Managing Azure Batch pools with Azure CLI](./batch-cli-sample-manage-pool.md) for more information on creating and deleting pools.</span></span>

```azurecli
az batch job delete --job-id myjob
```

## <a name="script-explanation"></a><span data-ttu-id="ec966-120">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="ec966-120">Script explanation</span></span>

<span data-ttu-id="ec966-121">Este script utiliza Hola después comandos toocreate un proceso por lotes y las tareas.</span><span class="sxs-lookup"><span data-stu-id="ec966-121">This script uses hello following commands toocreate a Batch job and tasks.</span></span> <span data-ttu-id="ec966-122">Cada comando de la tabla de hello vincula documentación específica del toocommand.</span><span class="sxs-lookup"><span data-stu-id="ec966-122">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="ec966-123">Comando</span><span class="sxs-lookup"><span data-stu-id="ec966-123">Command</span></span> | <span data-ttu-id="ec966-124">Notas</span><span class="sxs-lookup"><span data-stu-id="ec966-124">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ec966-125">az batch account login</span><span class="sxs-lookup"><span data-stu-id="ec966-125">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="ec966-126">Autenticarse en una cuenta de Batch.</span><span class="sxs-lookup"><span data-stu-id="ec966-126">Authenticate against a Batch account.</span></span>  |
| [<span data-ttu-id="ec966-127">az batch job create</span><span class="sxs-lookup"><span data-stu-id="ec966-127">az batch job create</span></span>](https://docs.microsoft.com/cli/azure/batch/job#create) | <span data-ttu-id="ec966-128">Crea un trabajo de Batch.</span><span class="sxs-lookup"><span data-stu-id="ec966-128">Creates a Batch job.</span></span>  |
| [<span data-ttu-id="ec966-129">az batch job set</span><span class="sxs-lookup"><span data-stu-id="ec966-129">az batch job set</span></span>](https://docs.microsoft.com/cli/azure/batch/job#set) | <span data-ttu-id="ec966-130">Actualiza las propiedades de un trabajo de Batch.</span><span class="sxs-lookup"><span data-stu-id="ec966-130">Updates properties of a Batch job.</span></span>  |
| [<span data-ttu-id="ec966-131">az batch job show</span><span class="sxs-lookup"><span data-stu-id="ec966-131">az batch job show</span></span>](https://docs.microsoft.com/cli/azure/batch/job#show) | <span data-ttu-id="ec966-132">Recupera los detalles de un trabajo de Batch especificado.</span><span class="sxs-lookup"><span data-stu-id="ec966-132">Retrieves details of a specified Batch job.</span></span>  |
| [<span data-ttu-id="ec966-133">az batch task create</span><span class="sxs-lookup"><span data-stu-id="ec966-133">az batch task create</span></span>](https://docs.microsoft.com/cli/azure/batch/task#create) | <span data-ttu-id="ec966-134">Agrega que una tarea toohello especifica el trabajo por lotes.</span><span class="sxs-lookup"><span data-stu-id="ec966-134">Adds a task toohello specified Batch job.</span></span>  |
| [<span data-ttu-id="ec966-135">az batch task show</span><span class="sxs-lookup"><span data-stu-id="ec966-135">az batch task show</span></span>](https://docs.microsoft.com/cli/azure/batch/task#show) | <span data-ttu-id="ec966-136">Recupera los detalles de Hola de una tarea de hello especifican trabajo por lotes.</span><span class="sxs-lookup"><span data-stu-id="ec966-136">Retrieves hello details of a task from hello specified Batch job.</span></span>  |
| [<span data-ttu-id="ec966-137">az batch task list</span><span class="sxs-lookup"><span data-stu-id="ec966-137">az batch task list</span></span>](https://docs.microsoft.com/cli/azure/batch/task#list) | <span data-ttu-id="ec966-138">Muestra las tareas de hello asociadas con el trabajo especificado Hola.</span><span class="sxs-lookup"><span data-stu-id="ec966-138">Lists hello tasks associated with hello specified job.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="ec966-139">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ec966-139">Next steps</span></span>

<span data-ttu-id="ec966-140">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ec966-140">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ec966-141">Encontrará más ejemplos de secuencias de comandos de CLI de lote en hello [documentación de CLI de lote de Azure](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ec966-141">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
