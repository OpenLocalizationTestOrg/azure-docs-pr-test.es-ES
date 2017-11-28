---
title: "Ejemplo de script de la CLI de Azure: escalado de un clúster de ACS | Microsoft Docs"
description: "Ejemplo de script de la CLI de Azure: escalado de un clúster de ACS"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, contenedores, microservicios, Kubernetes, DC/OS, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: nepeters
ms.openlocfilehash: 0ea2c73436e650fdb37535538baccc565369fa9d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="scale-an-azure-container-service-cluster"></a><span data-ttu-id="eb3e0-104">Escalado de un clúster de Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="eb3e0-104">Scale an Azure Container Service Cluster</span></span>

<span data-ttu-id="eb3e0-105">En este ejemplo se escala una instancia de Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="eb3e0-105">This sample scales and Azure Container Service.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="eb3e0-106">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="eb3e0-106">Sample script</span></span>

```azurecli
az acs scale --resource-group myResourceGroup --name myK8SCluster --new-agent-count 5
```

## <a name="clean-up-deployment"></a><span data-ttu-id="eb3e0-107">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="eb3e0-107">Clean up deployment</span></span> 

<span data-ttu-id="eb3e0-108">Ejecute el siguiente comando para quitar el grupo de recursos, la máquina virtual y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="eb3e0-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="eb3e0-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="eb3e0-109">Script explanation</span></span>

<span data-ttu-id="eb3e0-110">Este script usa los siguientes comandos para crear la implementación.</span><span class="sxs-lookup"><span data-stu-id="eb3e0-110">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="eb3e0-111">Cada elemento de la tabla incluye vínculos a la documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="eb3e0-111">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="eb3e0-112">Comando</span><span class="sxs-lookup"><span data-stu-id="eb3e0-112">Command</span></span> | <span data-ttu-id="eb3e0-113">Notas</span><span class="sxs-lookup"><span data-stu-id="eb3e0-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="eb3e0-114">az acs scale</span><span class="sxs-lookup"><span data-stu-id="eb3e0-114">az acs scale</span></span>](/cli/azure/acs#scale) | <span data-ttu-id="eb3e0-115">Escale un clúster de ACS.</span><span class="sxs-lookup"><span data-stu-id="eb3e0-115">Scale an ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="eb3e0-116">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="eb3e0-116">Next steps</span></span>

<span data-ttu-id="eb3e0-117">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="eb3e0-117">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="eb3e0-118">Puede encontrar ejemplos de script adicionales de la CLI de Azure Container Service en la [documentación de Azure Container Service](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="eb3e0-118">Additional Azure Container Service CLI script samples can be found in the [Azure Container Service documentation](../cli-samples.md).</span></span>

