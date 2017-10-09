---
title: Ejemplo de secuencia de comandos de CLI - aaaAzure escalar un Cluster ACS | Documentos de Microsoft
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
ms.openlocfilehash: b1c214d7cca615257ec8cd6e9993cd15f694289b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scale-an-azure-container-service-cluster"></a><span data-ttu-id="609cd-104">Escalado de un clúster de Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="609cd-104">Scale an Azure Container Service Cluster</span></span>

<span data-ttu-id="609cd-105">En este ejemplo se escala una instancia de Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="609cd-105">This sample scales and Azure Container Service.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="609cd-106">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="609cd-106">Sample script</span></span>

```azurecli
az acs scale --resource-group myResourceGroup --name myK8SCluster --new-agent-count 5
```

## <a name="clean-up-deployment"></a><span data-ttu-id="609cd-107">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="609cd-107">Clean up deployment</span></span> 

<span data-ttu-id="609cd-108">Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="609cd-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="609cd-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="609cd-109">Script explanation</span></span>

<span data-ttu-id="609cd-110">Este script utiliza Hola después de la implementación de comandos toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="609cd-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="609cd-111">Cada elemento de la documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="609cd-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="609cd-112">Comando</span><span class="sxs-lookup"><span data-stu-id="609cd-112">Command</span></span> | <span data-ttu-id="609cd-113">Notas</span><span class="sxs-lookup"><span data-stu-id="609cd-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="609cd-114">az acs scale</span><span class="sxs-lookup"><span data-stu-id="609cd-114">az acs scale</span></span>](/cli/azure/acs#scale) | <span data-ttu-id="609cd-115">Escale un clúster de ACS.</span><span class="sxs-lookup"><span data-stu-id="609cd-115">Scale an ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="609cd-116">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="609cd-116">Next steps</span></span>

<span data-ttu-id="609cd-117">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="609cd-117">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="609cd-118">Encontrará más ejemplos de secuencias de comandos de CLI de servicio de contenedor de Azure en hello [documentación del servicio de contenedor de Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="609cd-118">Additional Azure Container Service CLI script samples can be found in hello [Azure Container Service documentation](../cli-samples.md).</span></span>

