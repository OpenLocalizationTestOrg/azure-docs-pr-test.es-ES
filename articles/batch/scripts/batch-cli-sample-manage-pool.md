---
title: "Ejemplo de script de la CLI de Azure: administración de grupos en Batch | Microsoft Docs"
description: "Ejemplo de script de la CLI de Azure: administración de grupos en Batch"
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
ms.openlocfilehash: 2556b02459886390b803407c5cb828687229a44e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-batch-pools-with-azure-cli"></a><span data-ttu-id="916b0-103">Administración de grupos de Azure Batch con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="916b0-103">Managing Azure Batch pools with Azure CLI</span></span>

<span data-ttu-id="916b0-104">Estos scripts muestran algunas de las herramientas disponibles en la CLI de Azure para crear y administrar grupos de nodos de ejecución en el servicio de Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="916b0-104">These script demonstrates some of the tools available in the Azure CLI to create and manage pools of compute nodes in the Azure Batch service.</span></span>

> [!NOTE]
> <span data-ttu-id="916b0-105">Los comandos de este ejemplo crean máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="916b0-105">The commands in this sample create Azure virtual machines.</span></span> <span data-ttu-id="916b0-106">La ejecución de máquinas virtuales acumulará cargos en su cuenta.</span><span class="sxs-lookup"><span data-stu-id="916b0-106">Running VMs will accrue charges to your account.</span></span> <span data-ttu-id="916b0-107">Para minimizarlos, elimine las máquinas virtuales cuando termine de ejecutar el ejemplo.</span><span class="sxs-lookup"><span data-stu-id="916b0-107">To minimize these charges, delete the VMs once you're done running the sample.</span></span> <span data-ttu-id="916b0-108">Consulte el artículo sobre cómo [limpiar los grupos](#clean-up-pools).</span><span class="sxs-lookup"><span data-stu-id="916b0-108">See [Clean up pools](#clean-up-pools).</span></span>

<span data-ttu-id="916b0-109">Los grupos de Batch se pueden configurar de dos formas, ya sea con una configuración de Cloud Services (solo Windows) o una configuración de Virtual Machine (Windows y Linux).</span><span class="sxs-lookup"><span data-stu-id="916b0-109">Batch pools can be configured in two ways, either with a Cloud Services configuration (Windows only), or a Virtual Machine configuration (Windows and Linux).</span></span> <span data-ttu-id="916b0-110">Los scripts de ejemplo siguientes muestran cómo crear grupos con ambas configuraciones.</span><span class="sxs-lookup"><span data-stu-id="916b0-110">The sample scripts below show how to create pools with both configurations.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="916b0-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="916b0-111">Prerequisites</span></span>

- <span data-ttu-id="916b0-112">Instale la CLI de Azure con las instrucciones que se encuentran en la [guía de instalación de la CLI de Azure](https://docs.microsoft.com/cli/azure/install-azure-cli) si aún no lo ha hecho.</span><span class="sxs-lookup"><span data-stu-id="916b0-112">Install the Azure CLI using the instructions provided in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="916b0-113">Cree una cuenta de Batch si aún no tiene una.</span><span class="sxs-lookup"><span data-stu-id="916b0-113">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="916b0-114">Consulte [Creación de una cuenta de Batch con la CLI de Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) para ver un script de ejemplo que crea una cuenta.</span><span class="sxs-lookup"><span data-stu-id="916b0-114">See [Create a Batch account with the Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>
- <span data-ttu-id="916b0-115">Configure una aplicación para que se ejecute desde una tarea de inicio si aún no lo ha hecho.</span><span class="sxs-lookup"><span data-stu-id="916b0-115">Configure an application to run from a start task if you haven't yet done so.</span></span> <span data-ttu-id="916b0-116">Consulte [Adición de aplicaciones a Azure Batch con la CLI de Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) para ver un script de ejemplo que crea una aplicación y carga un paquete de aplicación en Azure.</span><span class="sxs-lookup"><span data-stu-id="916b0-116">See [Adding applications to Azure Batch with Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) for a sample script that creates an application and uploads an application package to Azure.</span></span>

## <a name="pool-with-cloud-service-configuration-sample-script"></a><span data-ttu-id="916b0-117">Grupo con script de ejemplo de configuración de Cloud Services</span><span class="sxs-lookup"><span data-stu-id="916b0-117">Pool with cloud service configuration sample script</span></span>

<span data-ttu-id="916b0-118">[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "Administración de grupos de Cloud Services")]</span><span class="sxs-lookup"><span data-stu-id="916b0-118">[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "Manage Cloud Services Pools")]</span></span>

## <a name="pool-with-virtual-machine-configuration-sample-script"></a><span data-ttu-id="916b0-119">Grupo con script de ejemplo de configuración de Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="916b0-119">Pool with virtual machine configuration sample script</span></span>

<span data-ttu-id="916b0-120">[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "Administración de grupos de Virtual Machine")]</span><span class="sxs-lookup"><span data-stu-id="916b0-120">[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "Manage Virtual Machine Pools")]</span></span>

## <a name="clean-up-pools"></a><span data-ttu-id="916b0-121">Limpieza de grupos</span><span class="sxs-lookup"><span data-stu-id="916b0-121">Clean up pools</span></span>

<span data-ttu-id="916b0-122">Después de ejecutar el script de ejemplo anterior, ejecute el comando siguiente para eliminar los grupos.</span><span class="sxs-lookup"><span data-stu-id="916b0-122">After you run the above sample script, run the following command to delete the pools.</span></span>
```azurecli
az batch pool delete --pool-id mypool-windows
az batch pool delete --pool-id mypool-linux
```

## <a name="script-explanation"></a><span data-ttu-id="916b0-123">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="916b0-123">Script explanation</span></span>

<span data-ttu-id="916b0-124">Este script usa los comandos siguientes para crear grupos de Batch y manipularlos.</span><span class="sxs-lookup"><span data-stu-id="916b0-124">This script uses the following commands to create and manipulate Batch pools.</span></span>
<span data-ttu-id="916b0-125">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="916b0-125">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="916b0-126">Comando</span><span class="sxs-lookup"><span data-stu-id="916b0-126">Command</span></span> | <span data-ttu-id="916b0-127">Notas</span><span class="sxs-lookup"><span data-stu-id="916b0-127">Notes</span></span> |
|---|---|
| [<span data-ttu-id="916b0-128">az batch account login</span><span class="sxs-lookup"><span data-stu-id="916b0-128">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="916b0-129">Autenticarse en una cuenta de Batch.</span><span class="sxs-lookup"><span data-stu-id="916b0-129">Authenticate against a Batch account.</span></span>  |
| [<span data-ttu-id="916b0-130">az batch application summary list</span><span class="sxs-lookup"><span data-stu-id="916b0-130">az batch application summary list</span></span>](https://docs.microsoft.com/cli/azure/batch/application/summary#list) | <span data-ttu-id="916b0-131">Enumerar las aplicaciones disponibles en la cuenta de Batch.</span><span class="sxs-lookup"><span data-stu-id="916b0-131">List the available applications in the Batch account.</span></span>  |
| [<span data-ttu-id="916b0-132">az batch pool create</span><span class="sxs-lookup"><span data-stu-id="916b0-132">az batch pool create</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#create) | <span data-ttu-id="916b0-133">Crear un grupo de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="916b0-133">Create a pool of VMs.</span></span>  |
| [<span data-ttu-id="916b0-134">az batch pool set</span><span class="sxs-lookup"><span data-stu-id="916b0-134">az batch pool set</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#set) | <span data-ttu-id="916b0-135">Actualizar propiedades de un grupo.</span><span class="sxs-lookup"><span data-stu-id="916b0-135">Update properties of a pool.</span></span>  |
| [<span data-ttu-id="916b0-136">az batch pool node-agent-skus list</span><span class="sxs-lookup"><span data-stu-id="916b0-136">az batch pool node-agent-skus list</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/node-agent-skus#list) | <span data-ttu-id="916b0-137">Enumerar la información disponible de imagen y SKU de agente del nodo.</span><span class="sxs-lookup"><span data-stu-id="916b0-137">List available node agent SKUs and image information.</span></span>  |
| [<span data-ttu-id="916b0-138">az batch pool resize</span><span class="sxs-lookup"><span data-stu-id="916b0-138">az batch pool resize</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#resize) | <span data-ttu-id="916b0-139">Cambiar la cantidad de máquinas virtuales en ejecución en el grupo especificado.</span><span class="sxs-lookup"><span data-stu-id="916b0-139">Resize the number of running VMs in the specified pool.</span></span>  |
| [<span data-ttu-id="916b0-140">az batch pool show</span><span class="sxs-lookup"><span data-stu-id="916b0-140">az batch pool show</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#show) | <span data-ttu-id="916b0-141">Mostrar las propiedades de un grupo.</span><span class="sxs-lookup"><span data-stu-id="916b0-141">Display the properties of a pool.</span></span>  |
| [<span data-ttu-id="916b0-142">az batch pool delete</span><span class="sxs-lookup"><span data-stu-id="916b0-142">az batch pool delete</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#delete) | <span data-ttu-id="916b0-143">Eliminar el grupo especificado.</span><span class="sxs-lookup"><span data-stu-id="916b0-143">Delete the specified pool.</span></span>  |
| [<span data-ttu-id="916b0-144">az batch pool autoscale enable</span><span class="sxs-lookup"><span data-stu-id="916b0-144">az batch pool autoscale enable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#enable) | <span data-ttu-id="916b0-145">Habilitar el escalado automático de un grupo y aplicar una fórmula.</span><span class="sxs-lookup"><span data-stu-id="916b0-145">Enable auto-scaling on a pool and apply a formula.</span></span>  |
| [<span data-ttu-id="916b0-146">az batch pool autoscale disable</span><span class="sxs-lookup"><span data-stu-id="916b0-146">az batch pool autoscale disable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#disable) | <span data-ttu-id="916b0-147">Deshabilitar el escalado automático de un grupo.</span><span class="sxs-lookup"><span data-stu-id="916b0-147">Disable auto-scaling on a pool.</span></span>  |
| [<span data-ttu-id="916b0-148">az batch node list</span><span class="sxs-lookup"><span data-stu-id="916b0-148">az batch node list</span></span>](https://docs.microsoft.com/cli/azure/batch/node#list) | <span data-ttu-id="916b0-149">Enumerar todos los nodos de ejecución del grupo especificado.</span><span class="sxs-lookup"><span data-stu-id="916b0-149">List all the compute node in the specified pool.</span></span>  |
| [<span data-ttu-id="916b0-150">az batch node reboot</span><span class="sxs-lookup"><span data-stu-id="916b0-150">az batch node reboot</span></span>](https://docs.microsoft.com/cli/azure/batch/node#reboot) | <span data-ttu-id="916b0-151">Reiniciar el nodo de ejecución especificado.</span><span class="sxs-lookup"><span data-stu-id="916b0-151">Reboot the specified compute node.</span></span>  |
| [<span data-ttu-id="916b0-152">az batch node delete</span><span class="sxs-lookup"><span data-stu-id="916b0-152">az batch node delete</span></span>](https://docs.microsoft.com/cli/azure/batch/node#delete) | <span data-ttu-id="916b0-153">Eliminar los nodos de la lista del grupo especificado.</span><span class="sxs-lookup"><span data-stu-id="916b0-153">Delete the listed nodes from the specified pool.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="916b0-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="916b0-154">Next steps</span></span>

<span data-ttu-id="916b0-155">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="916b0-155">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="916b0-156">Puede encontrar ejemplos de script adicionales de la CLI de Batch en la [documentación de la CLI de Azure Batch](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="916b0-156">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>

