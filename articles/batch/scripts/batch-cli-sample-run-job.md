---
title: "Ejemplo de script de la CLI de Azure - Ejecución de un trabajo con Batch | Microsoft Docs"
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
ms.openlocfilehash: 5fe1e3595d9459e60b2fd54d6f17f6822731f453
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="running-jobs-on-azure-batch-with-azure-cli"></a><span data-ttu-id="2f266-103">Ejecución de trabajos en Azure Batch con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="2f266-103">Running jobs on Azure Batch with Azure CLI</span></span>

<span data-ttu-id="2f266-104">Este script crea un trabajo de Batch y agrega una serie de tareas a dicho trabajo.</span><span class="sxs-lookup"><span data-stu-id="2f266-104">This script creates a Batch job and adds a series of tasks to the job.</span></span> <span data-ttu-id="2f266-105">También muestra cómo supervisar un trabajo y sus tareas.</span><span class="sxs-lookup"><span data-stu-id="2f266-105">It also demonstrates how to monitor a job and its tasks.</span></span> <span data-ttu-id="2f266-106">Finalmente, muestra cómo consultar el servicio Batch de forma eficaz para obtener información sobre las tareas del trabajo.</span><span class="sxs-lookup"><span data-stu-id="2f266-106">Finally, it shows how to query the Batch service efficiently for information about the job's tasks.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f266-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2f266-107">Prerequisites</span></span>

- <span data-ttu-id="2f266-108">Instale la CLI de Azure con las instrucciones que se encuentran en la [guía de instalación de la CLI de Azure](https://docs.microsoft.com/cli/azure/install-azure-cli) si aún no lo ha hecho.</span><span class="sxs-lookup"><span data-stu-id="2f266-108">Install the Azure CLI using the instructions provided in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="2f266-109">Cree una cuenta de Batch si aún no tiene una.</span><span class="sxs-lookup"><span data-stu-id="2f266-109">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="2f266-110">Consulte [Creación de una cuenta de Batch con la CLI de Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) para ver un script de ejemplo que crea una cuenta.</span><span class="sxs-lookup"><span data-stu-id="2f266-110">See [Create a Batch account with the Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>
- <span data-ttu-id="2f266-111">Configure una aplicación para que se ejecute desde una tarea de inicio si aún no lo ha hecho.</span><span class="sxs-lookup"><span data-stu-id="2f266-111">Configure an application to run from a start task if you haven't yet done so.</span></span> <span data-ttu-id="2f266-112">Consulte [Adición de aplicaciones a Azure Batch con la CLI de Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) para ver un script de ejemplo que crea una aplicación y carga un paquete de aplicación en Azure.</span><span class="sxs-lookup"><span data-stu-id="2f266-112">See [Adding applications to Azure Batch with Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) for a sample script that creates an application and uploads an application package to Azure.</span></span>
- <span data-ttu-id="2f266-113">Configure un grupo en el que se ejecutará el trabajo.</span><span class="sxs-lookup"><span data-stu-id="2f266-113">Configure a pool on which the job will run.</span></span> <span data-ttu-id="2f266-114">Consulte [Administración de grupos de Azure Batch con la CLI de Azure](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool) para ver un script de ejemplo que crea un grupo con una configuración de servicios en la nube o de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="2f266-114">See [Managing Azure Batch pools with Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool) for a sample script that creates a pool with either a Cloud Service Configuration or a Virtual Machine Configuration.</span></span>

## <a name="sample-script"></a><span data-ttu-id="2f266-115">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="2f266-115">Sample script</span></span>

<span data-ttu-id="2f266-116">[!code-azurecli[main](../../../cli_scripts/batch/run-job/run-job.sh "Ejecutar trabajo")]</span><span class="sxs-lookup"><span data-stu-id="2f266-116">[!code-azurecli[main](../../../cli_scripts/batch/run-job/run-job.sh "Run Job")]</span></span>

## <a name="clean-up-job"></a><span data-ttu-id="2f266-117">Limpieza de un trabajo</span><span class="sxs-lookup"><span data-stu-id="2f266-117">Clean up job</span></span>

<span data-ttu-id="2f266-118">Después de ejecutar el script de ejemplo anterior, ejecute el comando siguiente para quitar el trabajo y todas sus tareas.</span><span class="sxs-lookup"><span data-stu-id="2f266-118">After you run the above sample script, run the following command to remove the job and all of its tasks.</span></span> <span data-ttu-id="2f266-119">Tenga en cuenta que el grupo debe eliminarse por separado.</span><span class="sxs-lookup"><span data-stu-id="2f266-119">Note that the pool will need to be deleted separately.</span></span> <span data-ttu-id="2f266-120">Consulte [Administración de grupos de Azure Batch con la CLI de Azure](./batch-cli-sample-manage-pool.md) para obtener más información sobre cómo crear y eliminar grupos.</span><span class="sxs-lookup"><span data-stu-id="2f266-120">See [Managing Azure Batch pools with Azure CLI](./batch-cli-sample-manage-pool.md) for more information on creating and deleting pools.</span></span>

```azurecli
az batch job delete --job-id myjob
```

## <a name="script-explanation"></a><span data-ttu-id="2f266-121">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="2f266-121">Script explanation</span></span>

<span data-ttu-id="2f266-122">Este script usa los siguientes comandos para crear un trabajo de Batch y las tareas.</span><span class="sxs-lookup"><span data-stu-id="2f266-122">This script uses the following commands to create a Batch job and tasks.</span></span> <span data-ttu-id="2f266-123">Cada comando de la tabla crea un vínculo a documentación específica de comando.</span><span class="sxs-lookup"><span data-stu-id="2f266-123">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="2f266-124">Comando</span><span class="sxs-lookup"><span data-stu-id="2f266-124">Command</span></span> | <span data-ttu-id="2f266-125">Notas</span><span class="sxs-lookup"><span data-stu-id="2f266-125">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2f266-126">az batch account login</span><span class="sxs-lookup"><span data-stu-id="2f266-126">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="2f266-127">Autenticarse en una cuenta de Batch.</span><span class="sxs-lookup"><span data-stu-id="2f266-127">Authenticate against a Batch account.</span></span>  |
| [<span data-ttu-id="2f266-128">az batch job create</span><span class="sxs-lookup"><span data-stu-id="2f266-128">az batch job create</span></span>](https://docs.microsoft.com/cli/azure/batch/job#create) | <span data-ttu-id="2f266-129">Crea un trabajo de Batch.</span><span class="sxs-lookup"><span data-stu-id="2f266-129">Creates a Batch job.</span></span>  |
| [<span data-ttu-id="2f266-130">az batch job set</span><span class="sxs-lookup"><span data-stu-id="2f266-130">az batch job set</span></span>](https://docs.microsoft.com/cli/azure/batch/job#set) | <span data-ttu-id="2f266-131">Actualiza las propiedades de un trabajo de Batch.</span><span class="sxs-lookup"><span data-stu-id="2f266-131">Updates properties of a Batch job.</span></span>  |
| [<span data-ttu-id="2f266-132">az batch job show</span><span class="sxs-lookup"><span data-stu-id="2f266-132">az batch job show</span></span>](https://docs.microsoft.com/cli/azure/batch/job#show) | <span data-ttu-id="2f266-133">Recupera los detalles de un trabajo de Batch especificado.</span><span class="sxs-lookup"><span data-stu-id="2f266-133">Retrieves details of a specified Batch job.</span></span>  |
| [<span data-ttu-id="2f266-134">az batch task create</span><span class="sxs-lookup"><span data-stu-id="2f266-134">az batch task create</span></span>](https://docs.microsoft.com/cli/azure/batch/task#create) | <span data-ttu-id="2f266-135">Agrega una tarea al trabajo de Batch especificado.</span><span class="sxs-lookup"><span data-stu-id="2f266-135">Adds a task to the specified Batch job.</span></span>  |
| [<span data-ttu-id="2f266-136">az batch task show</span><span class="sxs-lookup"><span data-stu-id="2f266-136">az batch task show</span></span>](https://docs.microsoft.com/cli/azure/batch/task#show) | <span data-ttu-id="2f266-137">Recupera los detalles de una tarea del trabajo de Batch especificado.</span><span class="sxs-lookup"><span data-stu-id="2f266-137">Retrieves the details of a task from the specified Batch job.</span></span>  |
| [<span data-ttu-id="2f266-138">az batch task list</span><span class="sxs-lookup"><span data-stu-id="2f266-138">az batch task list</span></span>](https://docs.microsoft.com/cli/azure/batch/task#list) | <span data-ttu-id="2f266-139">Enumera las tareas asociadas con el trabajo especificado.</span><span class="sxs-lookup"><span data-stu-id="2f266-139">Lists the tasks associated with the specified job.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="2f266-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2f266-140">Next steps</span></span>

<span data-ttu-id="2f266-141">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2f266-141">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="2f266-142">Puede encontrar ejemplos de script adicionales de la CLI de Batch en la [documentación de la CLI de Azure Batch](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2f266-142">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
