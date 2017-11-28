---
title: aaaAzure ejemplo para quitar la secuencia de comandos de Service Fabric CLI
description: "Quitar una aplicación de un clúster de Azure Service Fabric mediante hello Azure Service Fabric CLI"
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
ms.openlocfilehash: 3ccefd4a04c5b7af71a2f959e11da6e402f25881
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a><span data-ttu-id="ec227-103">Eliminación de una aplicación de un clúster de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ec227-103">Remove an application from a Service Fabric cluster</span></span>

<span data-ttu-id="ec227-104">Este script de ejemplo elimina una instancia de la aplicación de Service Fabric ejecución, se anula el registro de un tipo de aplicación y la versión de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="ec227-104">This sample script deletes a running Service Fabric application instance, unregisters an application type and version from hello cluster.</span></span>  <span data-ttu-id="ec227-105">Instancia de la aplicación hello eliminar también elimina Hola todas las instancias de servicio asociadas a esa aplicación en ejecución.</span><span class="sxs-lookup"><span data-stu-id="ec227-105">Deleting hello application instance also deletes all hello running service instances associated with that application.</span></span> <span data-ttu-id="ec227-106">A continuación, se eliminan los archivos de aplicación Hola Hola almacén de imágenes.</span><span class="sxs-lookup"><span data-stu-id="ec227-106">Next, hello application files are deleted from hello image store.</span></span> 

<span data-ttu-id="ec227-107">Si es necesario, instale hello [Service Fabric CLI](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ec227-107">If needed, install hello [Service Fabric CLI](../service-fabric-cli.md).</span></span>

## <a name="sample-script"></a><span data-ttu-id="ec227-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="ec227-108">Sample script</span></span>

[!code-sh[main](../../../cli_scripts/service-fabric/remove-application/remove-application.sh "Remove an application from a cluster")]

## <a name="next-steps"></a><span data-ttu-id="ec227-109">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ec227-109">Next steps</span></span>

<span data-ttu-id="ec227-110">Para obtener más información, vea hello [documentación de Service Fabric CLI](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ec227-110">For more information, see hello [Service Fabric CLI documentation](../service-fabric-cli.md).</span></span>

<span data-ttu-id="ec227-111">Encontrará más ejemplos de CLI de tejido de servicio para Azure Service Fabric en hello [ejemplos de CLI de tejido de servicio](../samples-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ec227-111">Additional Service Fabric CLI samples for Azure Service Fabric can be found in hello [Service Fabric CLI samples](../samples-cli.md).</span></span>
