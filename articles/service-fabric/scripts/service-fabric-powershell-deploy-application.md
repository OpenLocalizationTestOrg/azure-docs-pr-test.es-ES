---
title: "Ejemplo de script de Azure PowerShell: implementar una aplicación en un clúster | Microsoft Docs"
description: "Ejemplo de script de Azure PowerShell: implementar una aplicación en un clúster de Service Fabric."
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
ms.openlocfilehash: 2863823205dbd70f63948ecd4af8898220fe1ff8
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2017
---
# <a name="deploy-an-application-to-a-service-fabric-cluster"></a><span data-ttu-id="4946c-103">Implementación de una aplicación en un clúster de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4946c-103">Deploy an application to a Service Fabric cluster</span></span>

<span data-ttu-id="4946c-104">Este script de ejemplo copia un paquete de aplicación en un almacén de imágenes de clúster, registra el tipo de aplicación en el clúster y crea una instancia de la aplicación a partir del tipo de aplicación.</span><span class="sxs-lookup"><span data-stu-id="4946c-104">This sample script copies an application package to a cluster image store, registers the application type in the cluster, and creates an application instance from the application type.</span></span>  <span data-ttu-id="4946c-105">Si se definieron servicios predeterminados en el manifiesto de aplicación del tipo de aplicación de destino, también se crean en este momento.</span><span class="sxs-lookup"><span data-stu-id="4946c-105">If any default services were defined in the application manifest of the target application type, then those services are created at this time.</span></span> <span data-ttu-id="4946c-106">Personalice los parámetros según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="4946c-106">Customize the parameters as needed.</span></span> 

<span data-ttu-id="4946c-107">Si es necesario, instale el módulo Service Fabric PowerShell con el [SDK de Service Fabric](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4946c-107">If needed, install the Service Fabric PowerShell module with the [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="4946c-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="4946c-108">Sample script</span></span>

<span data-ttu-id="4946c-109">[!code-powershell[main](../../../powershell_scripts/service-fabric/deploy-application/deploy-application.ps1 "Implementación de una aplicación en un clúster")]</span><span class="sxs-lookup"><span data-stu-id="4946c-109">[!code-powershell[main](../../../powershell_scripts/service-fabric/deploy-application/deploy-application.ps1 "Deploy an application to a cluster")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="4946c-110">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="4946c-110">Clean up deployment</span></span> 

<span data-ttu-id="4946c-111">Después de que el ejemplo de script se haya ejecutado, el script de [Remove an application](service-fabric-powershell-remove-application.md) (Quitar una aplicación) puede utilizarse para quitar la instancia de la aplicación, anular el registro del tipo de aplicación y eliminar el paquete de aplicación del almacén de imágenes.</span><span class="sxs-lookup"><span data-stu-id="4946c-111">After the script sample has been run, the script in [Remove an application](service-fabric-powershell-remove-application.md) can be used to remove the application instance, unregister the application type, and delete the application package from the image store.</span></span>

## <a name="script-explanation"></a><span data-ttu-id="4946c-112">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="4946c-112">Script explanation</span></span>

<span data-ttu-id="4946c-113">Este script usa los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="4946c-113">This script uses the following commands.</span></span> <span data-ttu-id="4946c-114">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="4946c-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="4946c-115">Comando</span><span class="sxs-lookup"><span data-stu-id="4946c-115">Command</span></span> | <span data-ttu-id="4946c-116">Notas</span><span class="sxs-lookup"><span data-stu-id="4946c-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4946c-117">Copy-ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="4946c-117">Copy-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="4946c-118">Copie un paquete de aplicación en el almacén de imágenes del clúster.</span><span class="sxs-lookup"><span data-stu-id="4946c-118">Copy an application package to the cluster image store.</span></span>  |
|[<span data-ttu-id="4946c-119">Register-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="4946c-119">Register-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps)| <span data-ttu-id="4946c-120">Registra el tipo y la versión de una aplicación en el clúster.</span><span class="sxs-lookup"><span data-stu-id="4946c-120">Registers an application type and version on the cluster.</span></span> |
|[<span data-ttu-id="4946c-121">New-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="4946c-121">New-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps)| <span data-ttu-id="4946c-122">Crea una aplicación a partir de un tipo de aplicación registrada.</span><span class="sxs-lookup"><span data-stu-id="4946c-122">Creates an application from a registered application type.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4946c-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4946c-123">Next steps</span></span>

<span data-ttu-id="4946c-124">Para más información sobre el módulo Service Fabric PowerShell, consulte la [documentación de Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="4946c-124">For more information on the Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="4946c-125">Puede encontrar ejemplos de PowerShell para Azure Service Fabric en los [ejemplos de Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4946c-125">Additional Powershell samples for Azure Service Fabric can be found in the [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
