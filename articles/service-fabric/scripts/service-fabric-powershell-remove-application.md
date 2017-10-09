---
title: "aaaAzure ejemplo de Script de PowerShell - quitar aplicación desde un clúster | Documentos de Microsoft"
description: "Ejemplo de script de Azure PowerShell: quitar una aplicación de un clúster de Service Fabric."
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
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 3fe2082c2fbeffbff1622f206021d4d907197d19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a><span data-ttu-id="1bed1-103">Eliminación de una aplicación de un clúster de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1bed1-103">Remove an application from a Service Fabric cluster</span></span>

<span data-ttu-id="1bed1-104">Este script de ejemplo elimina una instancia de la aplicación de Service Fabric ejecución, anula el registro de un tipo de aplicación y la versión de clúster de Hola y elimina el paquete de aplicación Hola Hola clúster del almacén de imágenes.</span><span class="sxs-lookup"><span data-stu-id="1bed1-104">This sample script deletes a running Service Fabric application instance, unregisters an application type and version from hello cluster, and deletes hello application package from hello cluster image store.</span></span>  <span data-ttu-id="1bed1-105">Instancia de la aplicación hello eliminar también elimina Hola todas las instancias de servicio asociadas a esa aplicación en ejecución.</span><span class="sxs-lookup"><span data-stu-id="1bed1-105">Deleting hello application instance also deletes all hello running service instances associated with that application.</span></span> <span data-ttu-id="1bed1-106">Personalizar los parámetros de hello según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="1bed1-106">Customize hello parameters as needed.</span></span> 

<span data-ttu-id="1bed1-107">Si es necesario, instale el módulo de PowerShell de tejido de servicio de hello con hello [SDK del servicio de Fabric](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1bed1-107">If needed, install hello Service Fabric PowerShell module with hello [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="1bed1-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="1bed1-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/remove-application/remove-application.ps1 "Remove an application from a cluster")]

## <a name="script-explanation"></a><span data-ttu-id="1bed1-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="1bed1-109">Script explanation</span></span>

<span data-ttu-id="1bed1-110">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="1bed1-110">This script uses hello following commands.</span></span> <span data-ttu-id="1bed1-111">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="1bed1-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="1bed1-112">Comando</span><span class="sxs-lookup"><span data-stu-id="1bed1-112">Command</span></span> | <span data-ttu-id="1bed1-113">Notas</span><span class="sxs-lookup"><span data-stu-id="1bed1-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1bed1-114">Remove-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="1bed1-114">Remove-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) | <span data-ttu-id="1bed1-115">Quita una instancia de la aplicación de Service Fabric ejecución de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="1bed1-115">Removes a running Service Fabric application instance from hello cluster.</span></span>  |
| [<span data-ttu-id="1bed1-116">Unregister-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="1bed1-116">Unregister-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="1bed1-117">Anula el registro de un tipo de aplicación de Service Fabric y una versión de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="1bed1-117">Unregisters a Service Fabric application type and version from hello cluster.</span></span> |
| [<span data-ttu-id="1bed1-118">Remove-ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="1bed1-118">Remove-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="1bed1-119">Quita un paquete de aplicación de Service Fabric Hola almacén de imágenes.</span><span class="sxs-lookup"><span data-stu-id="1bed1-119">Removes a Service Fabric application package from hello image store.</span></span>|

## <a name="next-steps"></a><span data-ttu-id="1bed1-120">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1bed1-120">Next steps</span></span>

<span data-ttu-id="1bed1-121">Para obtener más información sobre el módulo de PowerShell de tejido de servicio de hello, consulte [documentación de Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="1bed1-121">For more information on hello Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="1bed1-122">Encontrará más ejemplos de Powershell para Azure Service Fabric en hello [ejemplos de PowerShell de Azure](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1bed1-122">Additional Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
