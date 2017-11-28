---
title: aaaAzure ejemplo para implementar la secuencia de comandos de Service Fabric CLI
description: "Implementar un clúster de Azure Service Fabric tooan de aplicación con hello Azure Service Fabric CLI"
services: service-fabric
documentationcenter: 
author: Thraka
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
ms.openlocfilehash: aaec7042a4fd7ed32ad706cde70361f23d18fb48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-service-fabric-cluster"></a><span data-ttu-id="5c69c-103">Implementar un clúster de Service Fabric tooa de aplicación</span><span class="sxs-lookup"><span data-stu-id="5c69c-103">Deploy an application tooa Service Fabric cluster</span></span>

<span data-ttu-id="5c69c-104">Este script de ejemplo copia un almacén de imágenes de clúster de aplicación paquete tooa, registra el tipo de aplicación hello en clúster de Hola y crea una instancia de la aplicación del tipo de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="5c69c-104">This sample script copies an application package tooa cluster image store, registers hello application type in hello cluster, and creates an application instance from hello application type.</span></span> <span data-ttu-id="5c69c-105">En este momento también se crea cualquier servicio predeterminado.</span><span class="sxs-lookup"><span data-stu-id="5c69c-105">Any default services are also created at this time.</span></span>

<span data-ttu-id="5c69c-106">Si es necesario, instale hello [Service Fabric CLI](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5c69c-106">If needed, install hello [Service Fabric CLI](../service-fabric-cli.md).</span></span>

## <a name="sample-script"></a><span data-ttu-id="5c69c-107">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="5c69c-107">Sample script</span></span>

[!code-sh[main](../../../cli_scripts/service-fabric/deploy-application/deploy-application.sh "Deploy an application tooa cluster")]

## <a name="clean-up-deployment"></a><span data-ttu-id="5c69c-108">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="5c69c-108">Clean up deployment</span></span>

<span data-ttu-id="5c69c-109">Cuando haya finalizado, Hola [quitar](cli-remove-application.md) script puede ser la aplicación de hello tooremove usado.</span><span class="sxs-lookup"><span data-stu-id="5c69c-109">When done, hello [remove](cli-remove-application.md) script can be used tooremove hello application.</span></span> <span data-ttu-id="5c69c-110">script de Hola remove elimina la instancia de la aplicación hello, anula el registro de tipo de aplicación hello y elimina el paquete de aplicación Hola desde el almacén de imágenes.</span><span class="sxs-lookup"><span data-stu-id="5c69c-110">hello remove script deletes hello application instance, unregisters hello application type, and deletes hello application package from the image store.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c69c-111">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5c69c-111">Next steps</span></span>

<span data-ttu-id="5c69c-112">Para obtener más información, vea hello [documentación de Service Fabric CLI](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5c69c-112">For more information, see hello [Service Fabric CLI documentation](../service-fabric-cli.md).</span></span>

<span data-ttu-id="5c69c-113">Encontrará más ejemplos de CLI de tejido de servicio para Azure Service Fabric en hello [ejemplos de CLI de tejido de servicio](../samples-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5c69c-113">Additional Service Fabric CLI samples for Azure Service Fabric can be found in hello [Service Fabric CLI samples](../samples-cli.md).</span></span>
