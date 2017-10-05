---
title: "Ejemplo de eliminación de script de la CLI de Azure Service Fabric"
description: "Eliminación de una aplicación de un clúster de Azure Service Fabric mediante la CLI de Azure Service Fabric"
services: service-fabric
documentationcenter: 
author: thraka
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: adegeo
ms.custom: mvc
ms.openlocfilehash: d86f195d2c37a71e476c5ba4eec040dd46931d23
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a><span data-ttu-id="c55ac-103">Eliminación de una aplicación de un clúster de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c55ac-103">Remove an application from a Service Fabric cluster</span></span>

<span data-ttu-id="c55ac-104">Este script de ejemplo elimina una instancia de aplicación de Service Fabric en ejecución y anula el registro del tipo y la versión de una aplicación del clúster.</span><span class="sxs-lookup"><span data-stu-id="c55ac-104">This sample script deletes a running Service Fabric application instance, unregisters an application type and version from the cluster.</span></span>  <span data-ttu-id="c55ac-105">La eliminación de la instancia de la aplicación también elimina todas las instancias de servicio en ejecución asociadas a esa aplicación.</span><span class="sxs-lookup"><span data-stu-id="c55ac-105">Deleting the application instance also deletes all the running service instances associated with that application.</span></span> <span data-ttu-id="c55ac-106">A continuación, los archivos de aplicación se eliminan del almacén de imágenes.</span><span class="sxs-lookup"><span data-stu-id="c55ac-106">Next, the application files are deleted from the image store.</span></span> 

<span data-ttu-id="c55ac-107">Instale la [CLI de Service Fabric](../service-fabric-cli.md) si es necesario.</span><span class="sxs-lookup"><span data-stu-id="c55ac-107">If needed, install the [Service Fabric CLI](../service-fabric-cli.md).</span></span>

## <a name="sample-script"></a><span data-ttu-id="c55ac-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="c55ac-108">Sample script</span></span>

<span data-ttu-id="c55ac-109">[!code-sh[main](../../../cli_scripts/service-fabric/remove-application/remove-application.sh "Quitar una aplicación de un clúster")]</span><span class="sxs-lookup"><span data-stu-id="c55ac-109">[!code-sh[main](../../../cli_scripts/service-fabric/remove-application/remove-application.sh "Remove an application from a cluster")]</span></span>

## <a name="next-steps"></a><span data-ttu-id="c55ac-110">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c55ac-110">Next steps</span></span>

<span data-ttu-id="c55ac-111">Para más información, consulte la [documentación de la CLI de Service Fabric](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c55ac-111">For more information, see the [Service Fabric CLI documentation](../service-fabric-cli.md).</span></span>

<span data-ttu-id="c55ac-112">Puede encontrar ejemplos adicionales de la CLI de Service Fabric para Azure Service Fabric en los [ejemplos de la CLI de Service Fabric](../samples-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c55ac-112">Additional Service Fabric CLI samples for Azure Service Fabric can be found in the [Service Fabric CLI samples](../samples-cli.md).</span></span>
