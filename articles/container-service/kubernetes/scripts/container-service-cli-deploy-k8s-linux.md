---
title: "aaaAzure ejemplo de secuencia de comandos de CLI - crear clúster de ACS Linux Kubernetes | Documentos de Microsoft"
description: "Ejemplo de script de la CLI de Azure: creación de un clúster de ACS con Kubernetes para Linux"
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
ms.openlocfilehash: cf3798ea8b08e3fc32acb35dabab4b2fbea179dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-container-service-kubernetes-linux-cluster"></a><span data-ttu-id="1a389-104">Creación de un clúster de Azure Container Service con Kubernetes para Linux</span><span class="sxs-lookup"><span data-stu-id="1a389-104">Create an Azure Container Service Kubernetes Linux Cluster</span></span>

<span data-ttu-id="1a389-105">En este ejemplo se crea un clúster de Azure Container Service que ejecuta Kubernetes para los contenedores basados en Linux.</span><span class="sxs-lookup"><span data-stu-id="1a389-105">This sample creates an Azure Container Service cluster running Kubernetes for Linux based containers.</span></span>

[!INCLUDE [sample-cli-install](../../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="1a389-106">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="1a389-106">Sample script</span></span>

```azurecli
az group create --name myResourceGroup --location eastus

az acs create \
  --orchestrator-type kubernetes \
  --resource-group myResourceGroup \
  --name myK8SCluster \
  --generate-ssh-keys
```

## <a name="clean-up-deployment"></a><span data-ttu-id="1a389-107">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="1a389-107">Clean up deployment</span></span> 

<span data-ttu-id="1a389-108">Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="1a389-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="1a389-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="1a389-109">Script explanation</span></span>

<span data-ttu-id="1a389-110">Este script utiliza Hola después de la implementación de comandos toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="1a389-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="1a389-111">Cada elemento de la documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="1a389-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="1a389-112">Comando</span><span class="sxs-lookup"><span data-stu-id="1a389-112">Command</span></span> | <span data-ttu-id="1a389-113">Notas</span><span class="sxs-lookup"><span data-stu-id="1a389-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1a389-114">az group create</span><span class="sxs-lookup"><span data-stu-id="1a389-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="1a389-115">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="1a389-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1a389-116">az acs create</span><span class="sxs-lookup"><span data-stu-id="1a389-116">az acs create</span></span>](https://docs.microsoft.com/cli/azure/acs#create) | <span data-ttu-id="1a389-117">Crea un clúster de ACS.</span><span class="sxs-lookup"><span data-stu-id="1a389-117">Creates and ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1a389-118">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1a389-118">Next steps</span></span>

<span data-ttu-id="1a389-119">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1a389-119">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="1a389-120">Encontrará más ejemplos de secuencias de comandos de CLI de servicio de contenedor de Azure en hello [documentación del servicio de contenedor de Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1a389-120">Additional Azure Container Service CLI script samples can be found in hello [Azure Container Service documentation](../cli-samples.md).</span></span>

