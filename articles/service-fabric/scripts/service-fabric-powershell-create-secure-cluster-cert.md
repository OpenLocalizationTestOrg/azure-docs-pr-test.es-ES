---
title: "Ejemplo de script de Azure PowerShell: creación de un clúster de Service Fabric | Microsoft Docs"
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
ms.openlocfilehash: 7cbeb3da695af3815ba660f9cc2e3388abb6f87d
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2017
---
# <a name="create-a-service-fabric-cluster"></a><span data-ttu-id="630bc-103">Creación de un clúster de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="630bc-103">Create a Service Fabric cluster</span></span>

<span data-ttu-id="630bc-104">En este script de ejemplo se crea un clúster de Service Fabric de cinco nodos protegido con un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="630bc-104">This sample script creates a Service Fabric cluster a five-node cluster secured with an X.509 certificate.</span></span>  <span data-ttu-id="630bc-105">El comando crea un certificado autofirmado y lo carga en un nuevo almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="630bc-105">The command creates a self-signed certificate and uploads it to a new key vault.</span></span> <span data-ttu-id="630bc-106">El certificado también se copia en un directorio local.</span><span class="sxs-lookup"><span data-stu-id="630bc-106">The certificate is also copied to a local directory.</span></span>  <span data-ttu-id="630bc-107">Establezca el parámetro *-OS* para elegir la versión de Windows o Linux que se ejecuta en los nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="630bc-107">Set the *-OS* parameter to choose the version of Windows or Linux that runs on the cluster nodes.</span></span>  <span data-ttu-id="630bc-108">Personalice los parámetros según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="630bc-108">Customize the parameters as needed.</span></span>

<span data-ttu-id="630bc-109">Si es necesario, instale Azure PowerShell con la instrucción que se encuentra en la [guía de Azure PowerShell](/powershell/azure/overview) y luego ejecute `Login-AzureRmAccount` para crear una conexión con Azure.</span><span class="sxs-lookup"><span data-stu-id="630bc-109">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview) and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="630bc-110">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="630bc-110">Sample script</span></span>

<span data-ttu-id="630bc-111">[!code-powershell[principal](../../../powershell_scripts/service-fabric/create-secure-cluster/create-secure-cluster.ps1 "Creación de un clúster de Service Fabric")]</span><span class="sxs-lookup"><span data-stu-id="630bc-111">[!code-powershell[main](../../../powershell_scripts/service-fabric/create-secure-cluster/create-secure-cluster.ps1 "Create a Service Fabric cluster")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="630bc-112">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="630bc-112">Clean up deployment</span></span> 

<span data-ttu-id="630bc-113">Después de ejecutar el script de ejemplo, se puede usar el comando siguiente para quitar el grupo de recursos, el clúster y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="630bc-113">After the script sample has been run, the following command can be used to remove the resource group, cluster, and all related resources.</span></span>

```powershell
$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="script-explanation"></a><span data-ttu-id="630bc-114">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="630bc-114">Script explanation</span></span>

<span data-ttu-id="630bc-115">Este script usa los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="630bc-115">This script uses the following commands.</span></span> <span data-ttu-id="630bc-116">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="630bc-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="630bc-117">Comando</span><span class="sxs-lookup"><span data-stu-id="630bc-117">Command</span></span> | <span data-ttu-id="630bc-118">Notas</span><span class="sxs-lookup"><span data-stu-id="630bc-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="630bc-119">New-AzureRmServiceFabricCluster</span><span class="sxs-lookup"><span data-stu-id="630bc-119">New-AzureRmServiceFabricCluster</span></span>](/powershell/module/azurerm.servicefabric/New-AzureRmServiceFabricCluster) | <span data-ttu-id="630bc-120">Crea un clúster de Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="630bc-120">Creates a new Service Fabric cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="630bc-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="630bc-121">Next steps</span></span>

<span data-ttu-id="630bc-122">Para obtener más información sobre el módulo de Azure PowerShell, consulte la [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="630bc-122">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="630bc-123">Puede encontrar ejemplos de Azure PowerShell para Azure Service Fabric en los [ejemplos de PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="630bc-123">Additional Azure Powershell samples for Azure Service Fabric can be found in the [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
