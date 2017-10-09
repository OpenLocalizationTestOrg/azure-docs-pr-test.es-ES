---
title: "Ejemplo de Script de PowerShell - aaaAzure actualizar una aplicación de Service Fabric | Documentos de Microsoft"
description: "Script de ejemplo de Azure PowerShell: actualización de una aplicación de Service Fabric."
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
ms.date: 08/23/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 4f4777607bd6b35a76029e09ddb441006565d4cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-service-fabric-application"></a><span data-ttu-id="d1794-103">Actualización de una aplicación de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d1794-103">Upgrade a Service Fabric application</span></span>

<span data-ttu-id="d1794-104">Este script de ejemplo actualiza una ejecución tooversion de instancia de aplicación de Service Fabric 1.3.0.</span><span class="sxs-lookup"><span data-stu-id="d1794-104">This sample script upgrades a running Service Fabric application instance tooversion 1.3.0.</span></span> <span data-ttu-id="d1794-105">script de Hola copia el almacén de imágenes de hello nueva aplicación paquete toohello clúster, registra el tipo de aplicación Hola, inicia una actualización supervisada y comprueba continuamente el estado de actualización de hello hasta que la actualización Hola complete o se revierte.</span><span class="sxs-lookup"><span data-stu-id="d1794-105">hello script copies hello new application package toohello cluster image store, registers hello application type, starts a monitored upgrade, and continuously checks hello upgrade status until hello upgrade completes or rolls back.</span></span> <span data-ttu-id="d1794-106">Personalizar los parámetros de hello según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="d1794-106">Customize hello parameters as needed.</span></span> 

<span data-ttu-id="d1794-107">Si es necesario, instale el módulo de PowerShell de tejido de servicio de hello con hello [SDK del servicio de Fabric](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d1794-107">If needed, install hello Service Fabric PowerShell module with hello [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="d1794-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="d1794-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/upgrade-application/upgrade-application.ps1 "Upgrade an application")]

## <a name="script-explanation"></a><span data-ttu-id="d1794-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="d1794-109">Script explanation</span></span>

<span data-ttu-id="d1794-110">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="d1794-110">This script uses hello following commands.</span></span> <span data-ttu-id="d1794-111">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="d1794-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="d1794-112">Comando</span><span class="sxs-lookup"><span data-stu-id="d1794-112">Command</span></span> | <span data-ttu-id="d1794-113">Notas</span><span class="sxs-lookup"><span data-stu-id="d1794-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d1794-114">Get-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="d1794-114">Get-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps) | <span data-ttu-id="d1794-115">Obtiene todas las aplicaciones de hello en clúster de Service Fabric de Hola o una aplicación específica.</span><span class="sxs-lookup"><span data-stu-id="d1794-115">Gets all hello applications in hello Service Fabric cluster or a specific application.</span></span>  |
| [<span data-ttu-id="d1794-116">Get-ServiceFabricApplicationUpgrade</span><span class="sxs-lookup"><span data-stu-id="d1794-116">Get-ServiceFabricApplicationUpgrade</span></span>](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) | <span data-ttu-id="d1794-117">Obtiene el estado de saludo de una actualización de la aplicación de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d1794-117">Gets hello status of a Service Fabric application upgrade.</span></span> |
| [<span data-ttu-id="d1794-118">Get-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="d1794-118">Get-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="d1794-119">Obtiene tipos de aplicaciones de Service Fabric Hola registrados en el clúster de Service Fabric Hola.</span><span class="sxs-lookup"><span data-stu-id="d1794-119">Gets hello Service Fabric application types registered on hello Service Fabric cluster.</span></span> |
| [<span data-ttu-id="d1794-120">Unregister-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="d1794-120">Unregister-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="d1794-121">Anula el registro de un tipo de aplicación de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d1794-121">Unregisters a Service Fabric application type.</span></span>  |
| [<span data-ttu-id="d1794-122">Copy-ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="d1794-122">Copy-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="d1794-123">Copia una imagen de toohello del paquete de aplicación de Service Fabric almacén.</span><span class="sxs-lookup"><span data-stu-id="d1794-123">Copies a Service Fabric application package toohello image store.</span></span>  |
| [<span data-ttu-id="d1794-124">Register-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="d1794-124">Register-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="d1794-125">Registra un tipo de aplicación de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d1794-125">Registers a Service Fabric application type.</span></span> |
| [<span data-ttu-id="d1794-126">Start-ServiceFabricApplicationUpgrade</span><span class="sxs-lookup"><span data-stu-id="d1794-126">Start-ServiceFabricApplicationUpgrade</span></span>](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) | <span data-ttu-id="d1794-127">Actualiza una versión de tipo de Service Fabric aplicación toohello aplicación especificada.</span><span class="sxs-lookup"><span data-stu-id="d1794-127">Upgrades a Service Fabric application toohello specified application type version.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="d1794-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d1794-128">Next steps</span></span>

<span data-ttu-id="d1794-129">Para obtener más información sobre el módulo de PowerShell de tejido de servicio de hello, consulte [documentación de Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="d1794-129">For more information on hello Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="d1794-130">Encontrará más ejemplos de Powershell para Azure Service Fabric en hello [ejemplos de PowerShell de Azure](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d1794-130">Additional Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
