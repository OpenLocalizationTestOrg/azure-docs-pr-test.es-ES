---
title: "Script de ejemplo de Azure PowerShell: apertura del puerto de la aplicación abierta en el equilibrador de carga | Microsoft Docs"
description: "Script de ejemplo de Azure PowerShell: apertura de un puerto en el equilibrador de carga de Azure para una aplicación de Service Fabric."
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 2958bdef0889076249918608c04c66678fa80b97
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="open-an-application-port-in-the-azure-load-balancer"></a><span data-ttu-id="7c3d9-103">Apertura de un puerto de aplicación en el equilibrador de carga de Azure</span><span class="sxs-lookup"><span data-stu-id="7c3d9-103">Open an application port in the Azure load balancer</span></span>

<span data-ttu-id="7c3d9-104">Las aplicaciones de Service Fabric que se ejecutan en Azure se ubican detrás del equilibrador de carga de Azure.</span><span class="sxs-lookup"><span data-stu-id="7c3d9-104">A Service Fabric application running in Azure sits behind the Azure load balancer.</span></span> <span data-ttu-id="7c3d9-105">Este script de ejemplo abre un puerto en un equilibrador de carga de Azure para que una aplicación de Service Fabric se comunique con los clientes externos.</span><span class="sxs-lookup"><span data-stu-id="7c3d9-105">This sample script opens a port in an Azure load balancer so that a Service Fabric application can communicate with external clients.</span></span> <span data-ttu-id="7c3d9-106">Personalice los parámetros según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="7c3d9-106">Customize the parameters as needed.</span></span> 

<span data-ttu-id="7c3d9-107">Si es necesario, instale el módulo Service Fabric PowerShell con el [SDK de Service Fabric](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7c3d9-107">If needed, install the Service Fabric PowerShell module with the [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="7c3d9-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="7c3d9-108">Sample script</span></span>

<span data-ttu-id="7c3d9-109">[!code-powershell[main](../../../powershell_scripts/service-fabric/open-port-in-load-balancer/open-port-in-load-balancer.ps1 "Open a port in the load balancer")]</span><span class="sxs-lookup"><span data-stu-id="7c3d9-109">[!code-powershell[main](../../../powershell_scripts/service-fabric/open-port-in-load-balancer/open-port-in-load-balancer.ps1 "Open a port in the load balancer")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="7c3d9-110">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="7c3d9-110">Script explanation</span></span>

<span data-ttu-id="7c3d9-111">Este script usa los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="7c3d9-111">This script uses the following commands.</span></span> <span data-ttu-id="7c3d9-112">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="7c3d9-112">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="7c3d9-113">Comando</span><span class="sxs-lookup"><span data-stu-id="7c3d9-113">Command</span></span> | <span data-ttu-id="7c3d9-114">Notas</span><span class="sxs-lookup"><span data-stu-id="7c3d9-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7c3d9-115">Get-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="7c3d9-115">Get-AzureRmResource</span></span>](/powershell/module/azurerm.resources/get-azurermresource) | <span data-ttu-id="7c3d9-116">Obtiene un recurso de Azure.</span><span class="sxs-lookup"><span data-stu-id="7c3d9-116">Gets an Azure resource.</span></span>  |
| [<span data-ttu-id="7c3d9-117">Get-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="7c3d9-117">Get-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/get-azurermloadbalancer) | <span data-ttu-id="7c3d9-118">Obtiene el equilibrador de carga de Azure.</span><span class="sxs-lookup"><span data-stu-id="7c3d9-118">Gets the Azure load balancer.</span></span> |
| [<span data-ttu-id="7c3d9-119">Add-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="7c3d9-119">Add-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig) | <span data-ttu-id="7c3d9-120">Agrega una configuración de sondeo a un equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="7c3d9-120">Adds a probe configuration to a load balancer.</span></span>|
| [<span data-ttu-id="7c3d9-121">Get-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="7c3d9-121">Get-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/get-azurermloadbalancerprobeconfig) | <span data-ttu-id="7c3d9-122">Obtiene una configuración de sondeo para un equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="7c3d9-122">Gets a probe configuration for a load balancer.</span></span> |
| [<span data-ttu-id="7c3d9-123">Add-AzureRmLoadBalancerRuleConfig</span><span class="sxs-lookup"><span data-stu-id="7c3d9-123">Add-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig) | <span data-ttu-id="7c3d9-124">Agrega una configuración de regla a un equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="7c3d9-124">Adds a rule configuration to a load balancer.</span></span> |
| [<span data-ttu-id="7c3d9-125">Set-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="7c3d9-125">Set-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/set-azurermloadbalancer) | <span data-ttu-id="7c3d9-126">Establece el estado del objetivo para un equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="7c3d9-126">Sets the goal state for a load balancer.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7c3d9-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7c3d9-127">Next steps</span></span>

<span data-ttu-id="7c3d9-128">Para obtener más información sobre el módulo de Azure PowerShell, consulte la [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7c3d9-128">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="7c3d9-129">Puede encontrar ejemplos de PowerShell para Azure Service Fabric en los [ejemplos de Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7c3d9-129">Additional Powershell samples for Azure Service Fabric can be found in the [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
