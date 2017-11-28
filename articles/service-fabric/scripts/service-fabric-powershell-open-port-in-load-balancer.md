---
title: "Ejemplo de Script de PowerShell: puerto de la aplicación abierta en el equilibrador de carga aaaAzure | Documentos de Microsoft"
description: "Ejemplo de Script de PowerShell Azure - abrir un puerto en el equilibrador de carga de Azure de Hola para una aplicación de Service Fabric."
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
ms.openlocfilehash: 6acb28942851dce63f89f7de362b7cf1dc7b1fee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="open-an-application-port-in-hello-azure-load-balancer"></a><span data-ttu-id="4a24f-103">Abrir un puerto de la aplicación en el equilibrador de carga de Azure Hola</span><span class="sxs-lookup"><span data-stu-id="4a24f-103">Open an application port in hello Azure load balancer</span></span>

<span data-ttu-id="4a24f-104">Una aplicación de Service Fabric que se ejecuta en Azure se encuentra detrás de equilibrador de carga de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="4a24f-104">A Service Fabric application running in Azure sits behind hello Azure load balancer.</span></span> <span data-ttu-id="4a24f-105">Este script de ejemplo abre un puerto en un equilibrador de carga de Azure para que una aplicación de Service Fabric se comunique con los clientes externos.</span><span class="sxs-lookup"><span data-stu-id="4a24f-105">This sample script opens a port in an Azure load balancer so that a Service Fabric application can communicate with external clients.</span></span> <span data-ttu-id="4a24f-106">Personalizar los parámetros de hello según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="4a24f-106">Customize hello parameters as needed.</span></span> 

<span data-ttu-id="4a24f-107">Si es necesario, instale el módulo de PowerShell de tejido de servicio de hello con hello [SDK del servicio de Fabric](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4a24f-107">If needed, install hello Service Fabric PowerShell module with hello [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="4a24f-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="4a24f-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/open-port-in-load-balancer/open-port-in-load-balancer.ps1 "Open a port in hello load balancer")]

## <a name="script-explanation"></a><span data-ttu-id="4a24f-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="4a24f-109">Script explanation</span></span>

<span data-ttu-id="4a24f-110">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="4a24f-110">This script uses hello following commands.</span></span> <span data-ttu-id="4a24f-111">Cada comando de la tabla de hello vincula documentación específica del toocommand.</span><span class="sxs-lookup"><span data-stu-id="4a24f-111">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="4a24f-112">Comando</span><span class="sxs-lookup"><span data-stu-id="4a24f-112">Command</span></span> | <span data-ttu-id="4a24f-113">Notas</span><span class="sxs-lookup"><span data-stu-id="4a24f-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4a24f-114">Get-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="4a24f-114">Get-AzureRmResource</span></span>](/powershell/module/azurerm.resources/get-azurermresource) | <span data-ttu-id="4a24f-115">Obtiene un recurso de Azure.</span><span class="sxs-lookup"><span data-stu-id="4a24f-115">Gets an Azure resource.</span></span>  |
| [<span data-ttu-id="4a24f-116">Get-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="4a24f-116">Get-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/get-azurermloadbalancer) | <span data-ttu-id="4a24f-117">Obtiene el equilibrador de carga de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="4a24f-117">Gets hello Azure load balancer.</span></span> |
| [<span data-ttu-id="4a24f-118">Add-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="4a24f-118">Add-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig) | <span data-ttu-id="4a24f-119">Agrega un equilibrador de carga de tooa de configuración de sondeo.</span><span class="sxs-lookup"><span data-stu-id="4a24f-119">Adds a probe configuration tooa load balancer.</span></span>|
| [<span data-ttu-id="4a24f-120">Get-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="4a24f-120">Get-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/get-azurermloadbalancerprobeconfig) | <span data-ttu-id="4a24f-121">Obtiene una configuración de sondeo para un equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="4a24f-121">Gets a probe configuration for a load balancer.</span></span> |
| [<span data-ttu-id="4a24f-122">Add-AzureRmLoadBalancerRuleConfig</span><span class="sxs-lookup"><span data-stu-id="4a24f-122">Add-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig) | <span data-ttu-id="4a24f-123">Agrega un equilibrador de carga de tooa de configuración de regla.</span><span class="sxs-lookup"><span data-stu-id="4a24f-123">Adds a rule configuration tooa load balancer.</span></span> |
| [<span data-ttu-id="4a24f-124">Set-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="4a24f-124">Set-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/set-azurermloadbalancer) | <span data-ttu-id="4a24f-125">Conjuntos de Hola estado de objetivo de un equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="4a24f-125">Sets hello goal state for a load balancer.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4a24f-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4a24f-126">Next steps</span></span>

<span data-ttu-id="4a24f-127">Para obtener más información sobre el módulo de PowerShell de Azure de hello, consulte [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4a24f-127">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="4a24f-128">Encontrará más ejemplos de Powershell para Azure Service Fabric en hello [ejemplos de PowerShell de Azure](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4a24f-128">Additional Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
