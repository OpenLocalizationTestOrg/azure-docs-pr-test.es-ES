---
title: "Ejemplo de script de la CLI de Azure: creación de un clúster de ACS con Kubernetes para Windows | Microsoft Docs"
description: "Ejemplo de script de la CLI de Azure: creación de un clúster de ACS con Kubernetes para Windows"
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
ms.openlocfilehash: 3cba915e3cf3aaaeb3faf14c2000ca94f61d28a5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-container-service-kubernetes-windows-cluster"></a><span data-ttu-id="de169-104">Creación de un clúster de Azure Container Service con Kubernetes para Windows</span><span class="sxs-lookup"><span data-stu-id="de169-104">Create an Azure Container Service Kubernetes Windows Cluster</span></span>

<span data-ttu-id="de169-105">En este ejemplo se crea un clúster de Azure Container Service que ejecuta Kubernetes para los contenedores basados en Windows.</span><span class="sxs-lookup"><span data-stu-id="de169-105">This sample creates an Azure Container Service cluster running Kubernetes for Windows based containers.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="de169-106">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="de169-106">Sample script</span></span>

```azurecli
az group create --name myResourceGroup --location eastus

az acs create \
  --orchestrator-type kubernetes \
  --resource-group myResourceGroup \
  --name myK8SCluster \
  --generate-ssh-keys \
  --admin-username azureuser \
  --admin-password Password12 \
  --windows
```

## <a name="clean-up-deployment"></a><span data-ttu-id="de169-107">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="de169-107">Clean up deployment</span></span> 

<span data-ttu-id="de169-108">Ejecute el siguiente comando para quitar el grupo de recursos, la máquina virtual y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="de169-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="de169-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="de169-109">Script explanation</span></span>

<span data-ttu-id="de169-110">Este script usa los siguientes comandos para crear la implementación.</span><span class="sxs-lookup"><span data-stu-id="de169-110">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="de169-111">Cada elemento de la tabla incluye vínculos a la documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="de169-111">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="de169-112">Comando</span><span class="sxs-lookup"><span data-stu-id="de169-112">Command</span></span> | <span data-ttu-id="de169-113">Notas</span><span class="sxs-lookup"><span data-stu-id="de169-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="de169-114">az group create</span><span class="sxs-lookup"><span data-stu-id="de169-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="de169-115">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="de169-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="de169-116">az acs create</span><span class="sxs-lookup"><span data-stu-id="de169-116">az acs create</span></span>](https://docs.microsoft.com/cli/azure/acs#create) | <span data-ttu-id="de169-117">Crea un clúster de ACS.</span><span class="sxs-lookup"><span data-stu-id="de169-117">Creates and ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="de169-118">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="de169-118">Next steps</span></span>

<span data-ttu-id="de169-119">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="de169-119">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="de169-120">Puede encontrar ejemplos de script adicionales de la CLI de Azure Container Service en la [documentación de Azure Container Service](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="de169-120">Additional Azure Container Service CLI script samples can be found in the [Azure Container Service documentation](../cli-samples.md).</span></span>
