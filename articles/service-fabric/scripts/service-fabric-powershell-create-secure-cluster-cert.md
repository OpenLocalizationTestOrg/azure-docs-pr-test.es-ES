---
title: "aaaAzure ejemplo de Script de PowerShell: crear un clúster de Service Fabric | Documentos de Microsoft"
description: "Ejemplo de script de Azure PowerShell: creación de un clúster de Service Fabric."
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0f9c8bc5-3789-4eb3-8deb-ae6e2200795a
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 12fdc201bd51688cb850cd456b1e00442b79c22d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster"></a><span data-ttu-id="6c8c9-103">Creación de un clúster de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6c8c9-103">Create a Service Fabric cluster</span></span>

<span data-ttu-id="6c8c9-104">En este script de ejemplo se crea un clúster de Service Fabric de cinco nodos protegido con un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="6c8c9-104">This sample script creates a Service Fabric cluster a five-node cluster secured with an X.509 certificate.</span></span>  <span data-ttu-id="6c8c9-105">comando de Hello crea un certificado autofirmado y cargarlo tooa nuevo almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="6c8c9-105">hello command creates a self-signed certificate and uploads it tooa new key vault.</span></span> <span data-ttu-id="6c8c9-106">certificado de Hello también es tooa copiada de directorio local.</span><span class="sxs-lookup"><span data-stu-id="6c8c9-106">hello certificate is also copied tooa local directory.</span></span>  <span data-ttu-id="6c8c9-107">Conjunto hello *-OS* parámetro version de hello toochoose de Windows o Linux que se ejecuta en nodos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="6c8c9-107">Set hello *-OS* parameter toochoose hello version of Windows or Linux that runs on hello cluster nodes.</span></span>  <span data-ttu-id="6c8c9-108">Personalizar los parámetros de hello según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="6c8c9-108">Customize hello parameters as needed.</span></span>

<span data-ttu-id="6c8c9-109">Si es necesario, instale hello Azure PowerShell con hello instrucción se encuentra en hello [Guía de Azure PowerShell](/powershell/azure/overview) y, a continuación, ejecute `Login-AzureRmAccount` toocreate una conexión con Azure.</span><span class="sxs-lookup"><span data-stu-id="6c8c9-109">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview) and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="6c8c9-110">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="6c8c9-110">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/create-secure-cluster/create-secure-cluster.ps1 "Create a Service Fabric cluster")]

## <a name="clean-up-deployment"></a><span data-ttu-id="6c8c9-111">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="6c8c9-111">Clean up deployment</span></span> 

<span data-ttu-id="6c8c9-112">Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser grupo de recursos de hello tooremove usado, clúster y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="6c8c9-112">After hello script sample has been run, hello following command can be used tooremove hello resource group, cluster, and all related resources.</span></span>

```powershell
$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="script-explanation"></a><span data-ttu-id="6c8c9-113">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="6c8c9-113">Script explanation</span></span>

<span data-ttu-id="6c8c9-114">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="6c8c9-114">This script uses hello following commands.</span></span> <span data-ttu-id="6c8c9-115">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="6c8c9-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="6c8c9-116">Comando</span><span class="sxs-lookup"><span data-stu-id="6c8c9-116">Command</span></span> | <span data-ttu-id="6c8c9-117">Notas</span><span class="sxs-lookup"><span data-stu-id="6c8c9-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6c8c9-118">New-AzureRmServiceFabricCluster</span><span class="sxs-lookup"><span data-stu-id="6c8c9-118">New-AzureRmServiceFabricCluster</span></span>](/powershell/module/azurerm.servicefabric/New-AzureRmServiceFabricCluster) | <span data-ttu-id="6c8c9-119">Crea un clúster de Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6c8c9-119">Creates a new Service Fabric cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6c8c9-120">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6c8c9-120">Next steps</span></span>

<span data-ttu-id="6c8c9-121">Para obtener más información sobre el módulo de PowerShell de Azure de hello, consulte [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6c8c9-121">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="6c8c9-122">Encontrará más ejemplos de Azure Powershell para Azure Service Fabric en hello [ejemplos de PowerShell de Azure](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6c8c9-122">Additional Azure Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
