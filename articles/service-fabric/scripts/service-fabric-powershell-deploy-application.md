---
title: "Ejemplo de Script de PowerShell: aaaAzure implementar aplicación tooa clúster | Documentos de Microsoft"
description: "Script de Azure PowerShell de ejemplo: implementar un clúster de Service Fabric tooa de aplicación."
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
ms.openlocfilehash: b417c9908c72f016e930c43ff2d13e0cc5451f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-service-fabric-cluster"></a><span data-ttu-id="05cbb-103">Implementar un clúster de Service Fabric tooa de aplicación</span><span class="sxs-lookup"><span data-stu-id="05cbb-103">Deploy an application tooa Service Fabric cluster</span></span>

<span data-ttu-id="05cbb-104">Este script de ejemplo copia un almacén de imágenes de clúster de aplicación paquete tooa, registra el tipo de aplicación hello en clúster de Hola y crea una instancia de la aplicación del tipo de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="05cbb-104">This sample script copies an application package tooa cluster image store, registers hello application type in hello cluster, and creates an application instance from hello application type.</span></span>  <span data-ttu-id="05cbb-105">Si los servicios predeterminados se definieron en el manifiesto de aplicación Hola del tipo de aplicación de destino de hello, dichos servicios se crean en este momento.</span><span class="sxs-lookup"><span data-stu-id="05cbb-105">If any default services were defined in hello application manifest of hello target application type, then those services are created at this time.</span></span> <span data-ttu-id="05cbb-106">Personalizar los parámetros de hello según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="05cbb-106">Customize hello parameters as needed.</span></span> 

<span data-ttu-id="05cbb-107">Si es necesario, instale el módulo de PowerShell de tejido de servicio de hello con hello [SDK del servicio de Fabric](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="05cbb-107">If needed, install hello Service Fabric PowerShell module with hello [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="05cbb-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="05cbb-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/deploy-application/deploy-application.ps1 "Deploy an application tooa cluster")]

## <a name="clean-up-deployment"></a><span data-ttu-id="05cbb-109">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="05cbb-109">Clean up deployment</span></span> 

<span data-ttu-id="05cbb-110">Después de ejecutar el ejemplo de script de Hola, Hola script en [quitar una aplicación](service-fabric-powershell-remove-application.md) puede ser instancia de la aplicación hello tooremove usado, anular el registro del tipo de aplicación hello y eliminar paquete de aplicación Hola Hola almacén de imágenes.</span><span class="sxs-lookup"><span data-stu-id="05cbb-110">After hello script sample has been run, hello script in [Remove an application](service-fabric-powershell-remove-application.md) can be used tooremove hello application instance, unregister hello application type, and delete hello application package from hello image store.</span></span>

## <a name="script-explanation"></a><span data-ttu-id="05cbb-111">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="05cbb-111">Script explanation</span></span>

<span data-ttu-id="05cbb-112">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="05cbb-112">This script uses hello following commands.</span></span> <span data-ttu-id="05cbb-113">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="05cbb-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="05cbb-114">Comando</span><span class="sxs-lookup"><span data-stu-id="05cbb-114">Command</span></span> | <span data-ttu-id="05cbb-115">Notas</span><span class="sxs-lookup"><span data-stu-id="05cbb-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="05cbb-116">Copy-ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="05cbb-116">Copy-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="05cbb-117">Copie un almacén de imágenes de clúster de aplicación paquete toohello.</span><span class="sxs-lookup"><span data-stu-id="05cbb-117">Copy an application package toohello cluster image store.</span></span>  |
|[<span data-ttu-id="05cbb-118">Register-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="05cbb-118">Register-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps)| <span data-ttu-id="05cbb-119">Registra un tipo de aplicación y la versión en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="05cbb-119">Registers an application type and version on hello cluster.</span></span> |
|[<span data-ttu-id="05cbb-120">New-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="05cbb-120">New-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps)| <span data-ttu-id="05cbb-121">Crea una aplicación a partir de un tipo de aplicación registrada.</span><span class="sxs-lookup"><span data-stu-id="05cbb-121">Creates an application from a registered application type.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="05cbb-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="05cbb-122">Next steps</span></span>

<span data-ttu-id="05cbb-123">Para obtener más información sobre el módulo de PowerShell de tejido de servicio de hello, consulte [documentación de Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="05cbb-123">For more information on hello Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="05cbb-124">Encontrará más ejemplos de Powershell para Azure Service Fabric en hello [ejemplos de PowerShell de Azure](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="05cbb-124">Additional Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
