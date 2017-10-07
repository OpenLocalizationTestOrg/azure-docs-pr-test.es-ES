---
title: "Ejemplo de secuencia de comandos de CLI - aaaAzure de grupos de administración en el lote | Documentos de Microsoft"
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
ms.openlocfilehash: 6c9ca9515565aff42752231a080943be8e4c810b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-batch-pools-with-azure-cli"></a><span data-ttu-id="43b2e-103">Administración de grupos de Azure Batch con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="43b2e-103">Managing Azure Batch pools with Azure CLI</span></span>

<span data-ttu-id="43b2e-104">Estas secuencias de comandos muestra algunas de las herramientas de hello disponibles en hello toocreate de CLI de Azure y administrar grupos de nodos de proceso en el servicio de Azure Batch Hola.</span><span class="sxs-lookup"><span data-stu-id="43b2e-104">These script demonstrates some of hello tools available in hello Azure CLI toocreate and manage pools of compute nodes in hello Azure Batch service.</span></span>

> [!NOTE]
> <span data-ttu-id="43b2e-105">comandos de Hello en este ejemplo crean máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="43b2e-105">hello commands in this sample create Azure virtual machines.</span></span> <span data-ttu-id="43b2e-106">Máquinas virtuales en ejecución se acumularán cuenta tooyour de cargos.</span><span class="sxs-lookup"><span data-stu-id="43b2e-106">Running VMs will accrue charges tooyour account.</span></span> <span data-ttu-id="43b2e-107">toominimize estos cargos, eliminar hello las máquinas virtuales una vez que haya terminado el ejemplo hello en ejecución.</span><span class="sxs-lookup"><span data-stu-id="43b2e-107">toominimize these charges, delete hello VMs once you're done running hello sample.</span></span> <span data-ttu-id="43b2e-108">Consulte el artículo sobre cómo [limpiar los grupos](#clean-up-pools).</span><span class="sxs-lookup"><span data-stu-id="43b2e-108">See [Clean up pools](#clean-up-pools).</span></span>

<span data-ttu-id="43b2e-109">Los grupos de Batch se pueden configurar de dos formas, ya sea con una configuración de Cloud Services (solo Windows) o una configuración de Virtual Machine (Windows y Linux).</span><span class="sxs-lookup"><span data-stu-id="43b2e-109">Batch pools can be configured in two ways, either with a Cloud Services configuration (Windows only), or a Virtual Machine configuration (Windows and Linux).</span></span> <span data-ttu-id="43b2e-110">scripts de ejemplo de Hola a continuación muestran cómo toocreate grupos con ambas configuraciones.</span><span class="sxs-lookup"><span data-stu-id="43b2e-110">hello sample scripts below show how toocreate pools with both configurations.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="43b2e-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="43b2e-111">Prerequisites</span></span>

- <span data-ttu-id="43b2e-112">Instalación Hola CLI de Azure utilizando instrucciones de hello proporcionadas en hello [Guía de instalación de CLI de Azure](https://docs.microsoft.com/cli/azure/install-azure-cli), si aún no lo ha hecho.</span><span class="sxs-lookup"><span data-stu-id="43b2e-112">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="43b2e-113">Cree una cuenta de Batch si aún no tiene una.</span><span class="sxs-lookup"><span data-stu-id="43b2e-113">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="43b2e-114">Vea [crear una cuenta de lote con hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) para una secuencia de comandos de ejemplo que crea una cuenta.</span><span class="sxs-lookup"><span data-stu-id="43b2e-114">See [Create a Batch account with hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>
- <span data-ttu-id="43b2e-115">Configurar una toorun de aplicación de una tarea de inicio si aún no lo ha hecho.</span><span class="sxs-lookup"><span data-stu-id="43b2e-115">Configure an application toorun from a start task if you haven't yet done so.</span></span> <span data-ttu-id="43b2e-116">Vea [agregar aplicaciones tooAzure por lotes con Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) para una secuencia de comandos de ejemplo que crea una aplicación y carga un tooAzure del paquete de aplicación.</span><span class="sxs-lookup"><span data-stu-id="43b2e-116">See [Adding applications tooAzure Batch with Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) for a sample script that creates an application and uploads an application package tooAzure.</span></span>

## <a name="pool-with-cloud-service-configuration-sample-script"></a><span data-ttu-id="43b2e-117">Grupo con script de ejemplo de configuración de Cloud Services</span><span class="sxs-lookup"><span data-stu-id="43b2e-117">Pool with cloud service configuration sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "Manage Cloud Services Pools")]

## <a name="pool-with-virtual-machine-configuration-sample-script"></a><span data-ttu-id="43b2e-118">Grupo con script de ejemplo de configuración de Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="43b2e-118">Pool with virtual machine configuration sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "Manage Virtual Machine Pools")]

## <a name="clean-up-pools"></a><span data-ttu-id="43b2e-119">Limpieza de grupos</span><span class="sxs-lookup"><span data-stu-id="43b2e-119">Clean up pools</span></span>

<span data-ttu-id="43b2e-120">Después de ejecutar Hola por encima de la secuencia de comandos de ejemplo, ejecute hello siguientes grupos de comando toodelete Hola.</span><span class="sxs-lookup"><span data-stu-id="43b2e-120">After you run hello above sample script, run hello following command toodelete hello pools.</span></span>
```azurecli
az batch pool delete --pool-id mypool-windows
az batch pool delete --pool-id mypool-linux
```

## <a name="script-explanation"></a><span data-ttu-id="43b2e-121">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="43b2e-121">Script explanation</span></span>

<span data-ttu-id="43b2e-122">Este script utiliza Hola después toocreate de comandos y manipular grupos de proceso por lotes.</span><span class="sxs-lookup"><span data-stu-id="43b2e-122">This script uses hello following commands toocreate and manipulate Batch pools.</span></span>
<span data-ttu-id="43b2e-123">Cada comando de la tabla de hello vincula documentación específica del toocommand.</span><span class="sxs-lookup"><span data-stu-id="43b2e-123">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="43b2e-124">Comando</span><span class="sxs-lookup"><span data-stu-id="43b2e-124">Command</span></span> | <span data-ttu-id="43b2e-125">Notas</span><span class="sxs-lookup"><span data-stu-id="43b2e-125">Notes</span></span> |
|---|---|
| [<span data-ttu-id="43b2e-126">az batch account login</span><span class="sxs-lookup"><span data-stu-id="43b2e-126">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="43b2e-127">Autenticarse en una cuenta de Batch.</span><span class="sxs-lookup"><span data-stu-id="43b2e-127">Authenticate against a Batch account.</span></span>  |
| [<span data-ttu-id="43b2e-128">az batch application summary list</span><span class="sxs-lookup"><span data-stu-id="43b2e-128">az batch application summary list</span></span>](https://docs.microsoft.com/cli/azure/batch/application/summary#list) | <span data-ttu-id="43b2e-129">Enumerar las aplicaciones disponibles de Hola Hola cuenta de lote.</span><span class="sxs-lookup"><span data-stu-id="43b2e-129">List hello available applications in hello Batch account.</span></span>  |
| [<span data-ttu-id="43b2e-130">az batch pool create</span><span class="sxs-lookup"><span data-stu-id="43b2e-130">az batch pool create</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#create) | <span data-ttu-id="43b2e-131">Crear un grupo de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="43b2e-131">Create a pool of VMs.</span></span>  |
| [<span data-ttu-id="43b2e-132">az batch pool set</span><span class="sxs-lookup"><span data-stu-id="43b2e-132">az batch pool set</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#set) | <span data-ttu-id="43b2e-133">Actualizar propiedades de un grupo.</span><span class="sxs-lookup"><span data-stu-id="43b2e-133">Update properties of a pool.</span></span>  |
| [<span data-ttu-id="43b2e-134">az batch pool node-agent-skus list</span><span class="sxs-lookup"><span data-stu-id="43b2e-134">az batch pool node-agent-skus list</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/node-agent-skus#list) | <span data-ttu-id="43b2e-135">Enumerar la información disponible de imagen y SKU de agente del nodo.</span><span class="sxs-lookup"><span data-stu-id="43b2e-135">List available node agent SKUs and image information.</span></span>  |
| [<span data-ttu-id="43b2e-136">az batch pool resize</span><span class="sxs-lookup"><span data-stu-id="43b2e-136">az batch pool resize</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#resize) | <span data-ttu-id="43b2e-137">Número de Hola de cambio de tamaño de las máquinas virtuales en ejecución en hello especificado grupo.</span><span class="sxs-lookup"><span data-stu-id="43b2e-137">Resize hello number of running VMs in hello specified pool.</span></span>  |
| [<span data-ttu-id="43b2e-138">az batch pool show</span><span class="sxs-lookup"><span data-stu-id="43b2e-138">az batch pool show</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#show) | <span data-ttu-id="43b2e-139">Mostrar propiedades de Hola de un grupo.</span><span class="sxs-lookup"><span data-stu-id="43b2e-139">Display hello properties of a pool.</span></span>  |
| [<span data-ttu-id="43b2e-140">az batch pool delete</span><span class="sxs-lookup"><span data-stu-id="43b2e-140">az batch pool delete</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#delete) | <span data-ttu-id="43b2e-141">Eliminar Hola especificado grupo.</span><span class="sxs-lookup"><span data-stu-id="43b2e-141">Delete hello specified pool.</span></span>  |
| [<span data-ttu-id="43b2e-142">az batch pool autoscale enable</span><span class="sxs-lookup"><span data-stu-id="43b2e-142">az batch pool autoscale enable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#enable) | <span data-ttu-id="43b2e-143">Habilitar el escalado automático de un grupo y aplicar una fórmula.</span><span class="sxs-lookup"><span data-stu-id="43b2e-143">Enable auto-scaling on a pool and apply a formula.</span></span>  |
| [<span data-ttu-id="43b2e-144">az batch pool autoscale disable</span><span class="sxs-lookup"><span data-stu-id="43b2e-144">az batch pool autoscale disable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#disable) | <span data-ttu-id="43b2e-145">Deshabilitar el escalado automático de un grupo.</span><span class="sxs-lookup"><span data-stu-id="43b2e-145">Disable auto-scaling on a pool.</span></span>  |
| [<span data-ttu-id="43b2e-146">az batch node list</span><span class="sxs-lookup"><span data-stu-id="43b2e-146">az batch node list</span></span>](https://docs.microsoft.com/cli/azure/batch/node#list) | <span data-ttu-id="43b2e-147">Lista de todos los nodos de proceso de hello en hello especificado grupo.</span><span class="sxs-lookup"><span data-stu-id="43b2e-147">List all hello compute node in hello specified pool.</span></span>  |
| [<span data-ttu-id="43b2e-148">az batch node reboot</span><span class="sxs-lookup"><span data-stu-id="43b2e-148">az batch node reboot</span></span>](https://docs.microsoft.com/cli/azure/batch/node#reboot) | <span data-ttu-id="43b2e-149">Reinicie el nodo de cálculo especificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="43b2e-149">Reboot hello specified compute node.</span></span>  |
| [<span data-ttu-id="43b2e-150">az batch node delete</span><span class="sxs-lookup"><span data-stu-id="43b2e-150">az batch node delete</span></span>](https://docs.microsoft.com/cli/azure/batch/node#delete) | <span data-ttu-id="43b2e-151">Los nodos de hello enumerado de eliminación de hello especificar grupo.</span><span class="sxs-lookup"><span data-stu-id="43b2e-151">Delete hello listed nodes from hello specified pool.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="43b2e-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="43b2e-152">Next steps</span></span>

<span data-ttu-id="43b2e-153">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="43b2e-153">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="43b2e-154">Encontrará más ejemplos de secuencias de comandos de CLI de lote en hello [documentación de CLI de lote de Azure](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="43b2e-154">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>

